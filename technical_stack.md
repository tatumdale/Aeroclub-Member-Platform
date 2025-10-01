# Technical Stack
## Herefordshire Aeroclub Member Platform

---

## Technology Selection: Firebase-First Approach

**Decision:** Use Firebase (Google Cloud Platform) as the primary backend

**Rationale:** Balance between speed of development (critical for volunteer project), low operational costs, and future scalability to support the full platform vision.

---

## Core Technology Stack

| Layer | Technology | Version | Justification |
|-------|------------|---------|---------------|
| **Frontend Framework** | React | 18+ | Component-based, excellent ecosystem, team expertise |
| **Build Tool** | Vite | 5+ | Fast HMR, modern, better than CRA |
| **Styling** | Tailwind CSS | 3+ | Rapid development, mobile-first, consistent design |
| **UI Components** | Headless UI + Custom | Latest | Accessible, unstyled components we can theme |
| **Calendar** | React Big Calendar | 1.8+ | Mature, customizable, good mobile support |
| **Icons** | Lucide React | 0.263+ | Consistent, aviation-friendly icons |
| **Backend** | Firebase | 10+ | Managed backend, real-time, scales automatically |
| **Authentication** | Firebase Auth | 10+ | Secure, supports email/password, expandable |
| **Database** | Cloud Firestore | 10+ | NoSQL, real-time, generous free tier |
| **Functions** | Cloud Functions | 4+ | Serverless compute, scheduled jobs |
| **Hosting** | Firebase Hosting | 10+ | Global CDN, auto SSL, simple deployment |
| **Email** | SendGrid Extension | Latest | 100 emails/day free, reliable delivery |
| **Analytics** | Google Analytics 4 | Latest | Free, integrated with Firebase |
| **Version Control** | GitHub | - | Industry standard, CI/CD with Actions |

---

## Why Firebase? (vs. Traditional Stack)

### Comparison: Firebase vs. Traditional VPS

| Consideration | Firebase | Traditional (Node.js + PostgreSQL + VPS) |
|---------------|----------|-------------------------------------------|
| **Development Speed** | ⚡️ Fast (6-8 weeks MVP) | 🐌 Slower (10-12 weeks MVP) |
| **Initial Cost** | £0/month | £10-20/month (VPS) |
| **DevOps Complexity** | ✅ Minimal (managed) | ❌ High (server management, backups, updates) |
| **Scalability** | ✅ Automatic | 🔧 Manual (server upgrades) |
| **Real-time Capability** | ✅ Built-in | 🔧 Requires WebSockets setup |
| **Authentication** | ✅ Built-in | 🔧 Build from scratch |
| **Security** | ✅ Managed | 🔧 You manage |
| **Backup/Recovery** | ✅ Automatic | 🔧 Manual setup |
| **Mobile App Ready** | ✅ Same backend | 🔧 Requires API restructure |
| **Future Modules** | ⚡️ Quick to add | 🐌 Infrastructure work needed |
| **Vendor Lock-in** | ⚠️ Some risk | ✅ Full control |
| **5-Year Cost** | £660-£1,380 | £600-1,200 + DevOps time |

**Decision:** Firebase wins for volunteer project with limited technical resources and need for rapid delivery.

---

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                         USER DEVICES                        │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │   Desktop    │  │    Mobile    │  │    Tablet    │      │
│  │   Browser    │  │   Browser    │  │   Browser    │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
└───────────────────────┬─────────────────────────────────────┘
                        │ HTTPS
                        ▼
┌─────────────────────────────────────────────────────────────┐
│                   FIREBASE HOSTING (CDN)                    │
│                    React SPA (Static Assets)                │
└───────────────────────┬─────────────────────────────────────┘
                        │
        ┌───────────────┼───────────────┐
        │               │               │
        ▼               ▼               ▼
┌──────────────┐ ┌──────────────┐ ┌──────────────┐
│   Firebase   │ │    Cloud     │ │    Cloud     │
│     Auth     │ │  Firestore   │ │  Functions   │
│              │ │              │ │              │
│ • Email/Pass │ │ • users      │ │ • onCreate   │
│ • Sessions   │ │ • shifts     │ │ • onUpdate   │
│ • UID tokens │ │ • bookings   │ │ • scheduled  │
│              │ │ • roles      │ │ • webhooks   │
└──────────────┘ └──────────────┘ └──────┬───────┘
                                          │
                                          ▼
                                   ┌──────────────┐
                                   │   SendGrid   │
                                   │  Extension   │
                                   │              │
                                   │ • Email API  │
                                   └──────────────┘
```

---

## Frontend Architecture

### React Application Structure

```
src/
├── components/          # Reusable UI components
│   ├── ui/             # Base components (Button, Card, Modal)
│   ├── layout/         # Layout components (Sidebar, Header)
│   └── shared/         # Shared components (RoleSelector, Calendar)
├── modules/            # Feature modules
│   ├── volunteer/      # Volunteer management
│   │   ├── components/
│   │   ├── hooks/
│   │   ├── services/
│   │   └── pages/
│   ├── auth/           # Authentication
│   └── profile/        # User profiles
├── services/           # API services
│   ├── firebase.js     # Firebase initialization
│   ├── auth.service.js
│   ├── shift.service.js
│   └── booking.service.js
├── hooks/              # Custom React hooks
│   ├── useAuth.js
│   ├── useShifts.js
│   └── useBookings.js
├── contexts/           # React contexts
│   ├── AuthContext.jsx
│   └── ThemeContext.jsx
├── utils/              # Utility functions
│   ├── dates.js
│   ├── validation.js
│   └── constants.js
├── routes/             # Route configuration
│   └── index.jsx
└── App.jsx             # Root component
```

### Key Frontend Patterns

**1. Component Structure**
```javascript
// Example: ShiftCard component
import { Calendar, Clock, Users } from 'lucide-react';

export const ShiftCard = ({ shift, onBook }) => {
  return (
    <div className="shift-card">
      <div className="shift-header">
        <Calendar size={20} />
        <span>{formatDate(shift.date)}</span>
      </div>
      <div className="shift-body">
        <Clock size={16} />
        <span>{shift.shiftType}</span>
        <Users size={16} />
        <span>{shift.volunteersNeeded} needed</span>
      </div>
      <button onClick={() => onBook(shift.id)}>
        Book Shift
      </button>
    </div>
  );
};
```

**2. Custom Hooks**
```javascript
// useShifts.js - Reusable shift data logic
export const useShifts = (roleId, dateRange) => {
  const [shifts, setShifts] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    const unsubscribe = getShiftsRealtime(
      roleId, 
      dateRange, 
      (data) => {
        setShifts(data);
        setLoading(false);
      }
    );
    
    return () => unsubscribe();
  }, [roleId, dateRange]);

  return { shifts, loading };
};
```

**3. Service Layer**
```javascript
// shift.service.js - Firebase abstraction
import { collection, query, where, onSnapshot } from 'firebase/firestore';

export const getShiftsRealtime = (roleId, dateRange, callback) => {
  const q = query(
    collection(db, 'shifts'),
    where('roleId', '==', roleId),
    where('date', '>=', dateRange.start),
    where('date', '<=', dateRange.end)
  );
  
  return onSnapshot(q, (snapshot) => {
    const shifts = snapshot.docs.map(doc => ({
      id: doc.id,
      ...doc.data()
    }));
    callback(shifts);
  });
};
```

---

## Backend Architecture (Firebase)

### Cloud Firestore Structure

```javascript
// Root collections
/users                  // User profiles and auth data
/volunteerRoles        // Role definitions (Duty Pilot, Fire Crew, etc.)
/shifts                // Volunteer shift requirements
/bookings              // Member shift bookings
/blackoutDates         // Dates when shifts not needed
/notifications         // Email notification log
```

### Security Rules Pattern

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    
    // Helper functions
    function isAuthenticated() {
      return request.auth != null;
    }
    
    function isOpsManager() {
      return isAuthenticated() && 
             get(/databases/$(database)/documents/users/$(request.auth.uid))
               .data.role == 'operations_manager';
    }
    
    function isOwner(userId) {
      return isAuthenticated() && request.auth.uid == userId;
    }
    
    // Users: read all, write own, ops can write all
    match /users/{userId} {
      allow read: if isAuthenticated();
      allow create: if isOwner(userId);
      allow update: if isOwner(userId) || isOpsManager();
      allow delete: if isOpsManager();
    }
    
    // Shifts: read public, write ops only
    match /shifts/{shiftId} {
      allow read: if true; // Public calendar
      allow write: if isOpsManager();
    }
    
    // Bookings: read authenticated, create own, update own/ops
    match /bookings/{bookingId} {
      allow read: if isAuthenticated();
      allow create: if isAuthenticated();
      allow update: if isOwner(resource.data.userId) || isOpsManager();
      allow delete: if isOpsManager();
    }
  }
}
```

---

### Cloud Functions Architecture

```javascript
// functions/index.js
const functions = require('firebase-functions');
const admin = require('firebase-admin');

admin.initializeApp();

// Trigger: On booking created
exports.onBookingCreate = functions.firestore
  .document('bookings/{bookingId}')
  .onCreate(async (snap, context) => {
    const booking = snap.data();
    
    // 1. Check training status
    const isFullyTrained = await checkTrainingStatus(
      booking.userId, 
      booking.roleId
    );
    
    // 2. Check vacancy
    const hasVacancy = await checkVacancy(booking.shiftId);
    
    // 3. Auto-approve or set pending
    if (isFullyTrained && hasVacancy) {
      await snap.ref.update({ status: 'approved' });
      await sendConfirmationEmail(booking, 'approved');
    } else {
      await snap.ref.update({ status: 'pending' });
      await sendConfirmationEmail(booking, 'pending');
      await notifyOpsManager(booking);
    }
  });

// Scheduled: Daily coverage check (8am)
exports.dailyCoverageCheck = functions.pubsub
  .schedule('0 8 * * *')
  .timeZone('Europe/London')
  .onRun(async (context) => {
    const now = admin.firestore.Timestamp.now();
    const threeDaysFromNow = new Date(now.toDate());
    threeDaysFromNow.setDate(threeDaysFromNow.getDate() + 3);
    
    // Find uncovered shifts in next 3 days
    const uncoveredShifts = await getUncoveredShifts(
      now, 
      admin.firestore.Timestamp.fromDate(threeDaysFromNow)
    );
    
    if (uncoveredShifts.length > 0) {
      await sendCoverageAlert(uncoveredShifts);
    }
  });

// Scheduled: Shift reminders (hourly)
exports.shiftReminders = functions.pubsub
  .schedule('0 * * * *')
  .timeZone('Europe/London')
  .onRun(async (context) => {
    const now = admin.firestore.Timestamp.now();
    
    // 3-day reminders
    await sendReminders(now, 3, 'reminder_3day');
    
    // 24-hour reminders
    await sendReminders(now, 1, 'reminder_24hour');
  });

// HTTP Callable: Manual assignment
exports.assignMemberToShift = functions.https.onCall(
  async (data, context) => {
    // Verify ops manager
    if (!context.auth || !await isOpsManager(context.auth.uid)) {
      throw new functions.https.HttpsError(
        'permission-denied',
        'Only Operations Managers can assign members'
      );
    }
    
    const { shiftId, userId } = data;
    
    // Create booking with auto-approve
    const booking = await admin.firestore()
      .collection('bookings')
      .add({
        shiftId,
        userId,
        roleId: await getShiftRoleId(shiftId),
        status: 'approved',
        approvedBy: context.auth.uid,
        approvedAt: admin.firestore.FieldValue.serverTimestamp(),
        createdBy: context.auth.uid,
        createdAt: admin.firestore.FieldValue.serverTimestamp()
      });
    
    await sendConfirmationEmail({ ...data, id: booking.id }, 'approved');
    
    return { success: true, bookingId: booking.id };
  }
);
```

---

## Email System (SendGrid)

### Firebase Extension Configuration

```yaml
# Extension: firestore-send-email
# Collection: mail

# Document structure for email sending
/mail/{emailId}
  to: ['user@example.com']
  from: 'noreply@herefordshireaeroclub.co.uk'
  replyTo: 'operations@herefordshireaeroclub.co.uk'
  template:
    name: 'booking-confirmation'
    data:
      memberName: 'Sarah Thompson'
      shiftDate: '2026-03-15'
      shiftType: 'Morning'
      shiftTime: '08:30 - 13:00'
```

### Email Templates (SendGrid Dynamic Templates)

**Template IDs:**
- `d-xxxxx1`: Booking Confirmation (Auto-Approved)
- `d-xxxxx2`: Booking Confirmation (Pending)
- `d-xxxxx3`: Booking Approved
- `d-xxxxx4`: Booking Rejected
- `d-xxxxx5`: Shift Reminder (3 days)
- `d-xxxxx6`: Shift Reminder (24 hours)
- `d-xxxxx7`: Cancellation (to Ops Manager)
- `d-xxxxx8`: Coverage Alert (to Ops Manager)

---

## Development Environment

### Required Tools

```bash
# Node.js and npm
node --version  # v18+ required
npm --version   # v9+ required

# Firebase CLI
npm install -g firebase-tools
firebase --version  # v12+ required

# Git
git --version  # v2.30+ required
```

### Environment Setup

```bash
# Clone repository
git clone https://github.com/herefordshire-aeroclub/volunteer-platform
cd volunteer-platform

# Install dependencies
npm install

# Firebase configuration
firebase login
firebase use --add  # Select project

# Environment variables (.env.local)
VITE_FIREBASE_API_KEY=xxxxx
VITE_FIREBASE_AUTH_DOMAIN=xxxxx
VITE_FIREBASE_PROJECT_ID=xxxxx
VITE_FIREBASE_STORAGE_BUCKET=xxxxx
VITE_FIREBASE_MESSAGING_SENDER_ID=xxxxx
VITE_FIREBASE_APP_ID=xxxxx

# Run development server
npm run dev
# Opens at http://localhost:5173
```

---

## Deployment Pipeline

### CI/CD with GitHub Actions

```yaml
# .github/workflows/deploy.yml
name: Deploy to Firebase

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
          
      - name: Install dependencies
        run: npm ci
        
      - name: Run tests
        run: npm test
        
      - name: Build
        run: npm run build
        env:
          VITE_FIREBASE_API_KEY: ${{ secrets.FIREBASE_API_KEY }}
          # ... other env vars
          
      - name: Deploy to Firebase
        uses: FirebaseExtended/action-hosting-deploy@v0
        with:
          repoToken: '${{ secrets.GITHUB_TOKEN }}'
          firebaseServiceAccount: '${{ secrets.FIREBASE_SERVICE_ACCOUNT }}'
          channelId: live
          projectId: herefordshire-aeroclub
```

### Deployment Stages

```
Development → Staging → Production

1. Development (Local)
   - Local Firebase emulator
   - Test data
   - Fast iteration

2. Staging (Firebase Hosting Preview)
   - Real Firebase (test project)
   - Staging data
   - QA testing

3. Production (Firebase Hosting)
   - Production Firebase project
   - Live data
   - Monitored deployment
```

---

## Performance Optimization

### Frontend Optimization

**1. Code Splitting**
```javascript
// Lazy load modules
const VolunteerDashboard = lazy(() => 
  import('./modules/volunteer/VolunteerDashboard')
);

const OpsManagerDashboard = lazy(() => 
  import('./modules/ops/OpsManagerDashboard')
);

// Route-based code splitting
<Route path="/volunteer" element={
  <Suspense fallback={<Loading />}>
    <VolunteerDashboard />
  </Suspense>
} />
```

**2. Image Optimization**
- Use WebP format with fallbacks
- Lazy load images below fold
- Serve responsive images
- Compress with imagemin

**3. Bundle Size**
- Target: <200KB initial bundle (gzipped)
- Tree-shake unused code
- Use production builds
- Monitor with webpack-bundle-analyzer

---

### Backend Optimization

**1. Firestore Indexes**
```javascript
// firestore.indexes.json
{
  "indexes": [
    {
      "collectionGroup": "shifts",
      "queryScope": "COLLECTION",
      "fields": [
        { "fieldPath": "roleId", "order": "ASCENDING" },
        { "fieldPath": "date", "order": "ASCENDING" },
        { "fieldPath": "status", "order": "ASCENDING" }
      ]
    },
    {
      "collectionGroup": "bookings",
      "queryScope": "COLLECTION",
      "fields": [
        { "fieldPath": "userId", "order": "ASCENDING" },
        { "fieldPath": "createdAt", "order": "DESCENDING" }
      ]
    }
  ]
}
```

**2. Query Optimization**
- Use composite indexes for complex queries
- Limit query results (pagination)
- Cache frequently accessed data
- Use Firestore real-time sparingly (subscribe only to active views)

**3. Cloud Functions**
- Use latest Node.js runtime (Node 18)
- Set appropriate memory allocation
- Use Cloud Firestore triggers efficiently
- Implement retry logic for external APIs

---

## Security Architecture

### Authentication Flow

```
1. User enters email/password
   ↓
2. Firebase Auth validates
   ↓
3. Returns JWT token (ID token)
   ↓
4. Frontend stores token (memory only, not localStorage)
   ↓
5. All API requests include token in header
   ↓
6. Firebase validates token server-side
   ↓
7. Firestore Security Rules check permissions
   ↓
8. Grant/deny access
```

### Data Protection

**1. Transport Security**
- HTTPS enforced (Firebase Hosting)
- TLS 1.2+ required
- HSTS headers enabled

**2. Authentication Security**
- Password requirements: 8+ chars, 1 uppercase, 1 number
- Email verification optional (Phase 1), required (Phase 2)
- Session management: 30-day timeout
- No sensitive data in JWT claims

**3. Authorization**
- Role-based access (member, ops_manager, committee)
- Field-level security in Firestore rules
- Server-side validation in Cloud Functions

**4. Data Privacy (GDPR)**
- User consent for data collection
- Data export capability
- Account deletion capability
- Audit logs (who accessed what, when)

---

## Monitoring & Observability

### Firebase Monitoring

```javascript
// Performance monitoring
import { getPerformance } from 'firebase/performance';
const perf = getPerformance(app);

// Custom traces
const trace = perf.trace('shift_booking_flow');
trace.start();
// ... booking logic
trace.stop();

// Error tracking
import { getAnalytics, logEvent } from 'firebase/analytics';
const analytics = getAnalytics(app);

logEvent(analytics, 'booking_error', {
  error_type: 'validation_failed',
  shift_id: shiftId
});
```

### Alerts Configuration

**Critical Alerts:**
- Firebase Hosting downtime
- Cloud Functions errors >5% in 5 minutes
- Firestore read/write errors spike
- Authentication failures spike
- Email delivery failures

**Warning Alerts:**
- Approaching Firebase quota limits
- Slow Cloud Functions (>3s p95 latency)
- High Firestore costs (>£10/day)

---

## Testing Strategy

### Test Pyramid

```
       ┌─────────────┐
       │   E2E (5%)  │  Cypress
       ├─────────────┤
       │ Integration │  React Testing Library
       │    (25%)    │  + Firebase Emulator
       ├─────────────┤
       │    Unit     │  Jest + Vitest
       │    (70%)    │  
       └─────────────┘
```

### Example Tests

**1. Unit Test (Service Layer)**
```javascript
// shift.service.test.js
import { getShifts } from './shift.service';
import { mockFirestore } from '../test-utils';

describe('getShifts', () => {
  it('should return shifts for given role and date range', async () => {
    const mockShifts = [
      { id: '1', roleId: 'duty-pilot', date: '2026-03-15' }
    ];
    mockFirestore.collection('shifts').get.mockResolvedValue(mockShifts);
    
    const result = await getShifts('duty-pilot', {
      start: '2026-03-01',
      end: '2026-03-31'
    });
    
    expect(result).toEqual(mockShifts);
  });
});
```

**2. Integration Test (React Component)**
```javascript
// ShiftCard.test.jsx
import { render, screen, fireEvent } from '@testing-library/react';
import { ShiftCard } from './ShiftCard';

describe('ShiftCard', () => {
  it('should call onBook when button clicked', () => {
    const mockOnBook = jest.fn();
    const shift = {
      id: '1',
      date: '2026-03-15',
      shiftType: 'morning',
      volunteersNeeded: 1
    };
    
    render(<ShiftCard shift={shift} onBook={mockOnBook} />);
    
    const bookButton = screen.getByText('Book Shift');
    fireEvent.click(bookButton);
    
    expect(mockOnBook).toHaveBeenCalledWith('1');
  });
});
```

**3. E2E Test (Cypress)**
```javascript
// shift-booking.cy.js
describe('Shift Booking Flow', () => {
  it('should allow member to book an available shift', () => {
    cy.visit('/');
    cy.login('sarah@example.com', 'password123');
    
    cy.contains('Available Shifts').click();
    cy.get('[data-testid="shift-card"]').first().click();
    cy.contains('Book Shift').click();
    
    cy.contains('Booking confirmed').should('be.visible');
    cy.get('[data-testid="my-shifts"]').should('contain', 'Morning - March 15');
  });
});
```

---

## Scalability Considerations

### Current Scale (Phase 1)
- **Users**: 100-200 members
- **Shifts**: ~50-100 per month
- **Bookings**: ~150-200 per month
- **Emails**: ~500-1000 per month

**Firebase Free Tier Coverage**: ✅ Complete

---

### Future Scale (Year 3-5)
- **Users**: 500 members
- **Shifts**: ~200 per month (multiple roles)
- **Bookings**: ~500 per month
- **Emails**: ~2000 per month
- **Payments**: ~800 transactions per month

**Estimated Costs**: £20-40/month

---

### Scaling Strategy

**If costs exceed budget:**
1. **Optimize first** (indexes, caching, query efficiency)
2. **Selective migration** (move high-volume reads to Cloud Storage + CDN)
3. **Full migration** (PostgreSQL + VPS - last resort)

**Migration path exists** but not needed for 3-5 year timeline.

---

## Browser Support

### Target Browsers

| Browser | Version | Support Level |
|---------|---------|---------------|
| Chrome | Last 2 versions | Full |
| Firefox | Last 2 versions | Full |
| Safari | Last 2 versions | Full |
| Edge | Last 2 versions | Full |
| Mobile Safari (iOS) | iOS 14+ | Full |
| Chrome (Android) | Android 10+ | Full |
| IE 11 | ❌ | Not supported |

---

## Accessibility Standards

**Target**: WCAG 2.1 Level AA compliance

**Key Requirements:**
- Semantic HTML
- ARIA labels on interactive elements
- Keyboard navigation (Tab, Enter, Escape)
- Focus indicators visible
- Color contrast ratio ≥4.5:1 (text)
- Text resizable to 200%
- Screen reader tested (NVDA, JAWS, VoiceOver)

---

## Technology Roadmap

### Phase 1-3 (Year 1)
- ✅ React 18 + Vite + Tailwind
- ✅ Firebase (Auth, Firestore, Functions, Hosting)
- ✅ SendGrid email

### Phase 4 (Year 2)
- ➕ Firebase Storage (document uploads)
- ➕ Algolia (advanced search - if needed)

### Phase 5 (Year 2)
- ➕ Stripe Extension (payments)
- ➕ Cloud Storage (file attachments)

### Phase 6+ (Year 3-5)
- 🔮 React Native (mobile apps)
- 🔮 Firebase Cloud Messaging (push notifications)
- 🔮 BigQuery (advanced analytics)
- 🔮 Cloud Run (custom API services if needed)

---

*Document Version: 1.0*  
*Last Updated: October 1, 2025*  
*Part of: Herefordshire Aeroclub Member Platform Specification*