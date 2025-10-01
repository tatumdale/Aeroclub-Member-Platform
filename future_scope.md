# Future Scope & Roadmap
## Herefordshire Aeroclub Member Platform - Phases 2-6+

---

## Document Purpose

This document outlines the future evolution of the Herefordshire Aeroclub Member Platform beyond Phase 1 (Volunteer Management). It provides:

- **Product roadmap** across multiple development phases
- **Feature descriptions** for future modules
- **Timeline estimates** and dependencies
- **Technical considerations** for expansion
- **Decision criteria** for prioritization

**Current Status**: Phase 1 (Volunteer Management) in development  
**Timeline Horizon**: 3-5 years (2025-2030)

---

## Product Evolution Strategy

### Phased Delivery Approach

```
PHASE 1          PHASE 2-3        PHASE 4          PHASE 5          PHASE 6+
(6-8 weeks)      (3-6 months)     (2-3 months)     (2-3 months)     (Ongoing)
┌──────────┐     ┌──────────┐     ┌──────────┐     ┌──────────┐     ┌──────────┐
│Volunteer │ →   │Multi-Role│ →   │Aircraft  │ →   │Payments &│ →   │Full      │
│Mgmt      │     │Expansion │     │Booking   │     │Billing   │     │Platform  │
│          │     │          │     │          │     │          │     │          │
│• Duty    │     │• Fire    │     │• Book    │     │• Member  │     │• Docs    │
│  Pilot   │     │  Crew    │     │  aircraft│     │  payments│     │• Flight  │
│• Training│     │• Basic   │     │• Conflict│     │• Flying  │     │  logs    │
│• Booking │     │  CRM     │     │  detect  │     │  fees    │     │• Mobile  │
│• Alerts  │     │• Reports │     │• Calendar│     │• Stripe  │     │• Advanced│
│          │     │          │     │  sync    │     │• Invoices│     │  reports │
└──────────┘     └──────────┘     └──────────┘     └──────────┘     └──────────┘

VALIDATE         VALIDATE         VALIDATE         VALIDATE         OPTIMIZE
↓                ↓                ↓                ↓                ↓
Does volunteer   Does multi-role  Does booking     Does online      Does complete
system work?     scale?           integrate well?  payment work?    platform deliver?
```

---

## Phase 2: Enhanced Volunteer Management & Basic CRM
**Timeline**: Weeks 7-9 (2-3 months post-Phase 1 launch)  
**Development Effort**: 40-50 hours  
**Operational Cost**: £0-10/month

### Goals
1. Proactive coverage management through advanced alerting
2. Prepare for Fire Crew role launch
3. Basic member CRM capabilities for better planning

---

### Features

#### F2.1: Advanced Alerting System
**Priority**: P0 (Critical for operations)

**Description**: Enhanced notification system beyond Phase 1 reminders.

**Capabilities**:
- **3-day and 24-hour shift reminders** (automated)
- **Coverage gap alerts** when shifts uncovered within 3 days
- **Cancellation notifications** to Ops Manager with suggested replacements
- **Bulk notifications** to members by role interest or availability

**User Stories**:
- "As Ops Manager, I want daily summary emails of upcoming coverage gaps"
- "As Ops Manager, I want to email all members interested in Fire Crew"
- "As member, I want SMS alerts for urgent last-minute coverage needs" (Phase 3)

**Technical Implementation**:
- Cloud Function scheduled tasks (hourly, daily)
- SendGrid API for bulk emails
- Notification preferences in user profiles (Phase 3)

---

#### F2.2: Role Interest Tracking & Reports
**Priority**: P0 (Required for Fire Crew planning)

**Description**: System to track and report on member interest in future volunteer roles.

**Capabilities**:
- **Role interest dashboard** showing members interested per role
- **Exportable reports** with contact info, availability, current activity
- **Email integration** to notify interested members when role launches
- **Interest analytics** (how many members needed before launch?)

**User Stories**:
- "As Ops Manager, I want to see which members are interested in Fire Crew"
- "As Committee, I need data to decide if Fire Crew is viable"
- "As member, I want to be notified when Fire Crew role is available"

**Technical Implementation**:
- `roleInterests` array in user profiles
- Report generation Cloud Functions
- Email notification queue for role launches

---

#### F2.3: Basic Member CRM
**Priority**: P1 (Should have for planning)

**Description**: Extended member profiles beyond Phase 1 volunteer data.

**New Fields**:
- **Membership tier** (Full, Student, Social)
- **Membership expiry date**
- **Pilot licence information** (type, number, expiry - optional)
- **Medical expiry** (optional)
- **Member tags** (e.g., "Instructor", "Committee", "New Member")
- **Member status** (Active, Inactive, Lapsed)

**Capabilities**:
- **Advanced filtering** (show me all active PPL holders)
- **Membership renewal reminders** (automated emails 30/14/7 days before expiry)
- **Member lifecycle tracking** (joined date, last activity, renewal history)
- **Bulk operations** (email all lapsed members)

**User Stories**:
- "As Ops Manager, I want to see which members' medical certificates are expiring soon"
- "As Committee, I want a list of all lapsed memberships for re-engagement"
- "As member, I want automatic renewal reminders"

**Technical Implementation**:
- Extend `users` collection with new fields
- Cloud Functions for renewal reminders
- Enhanced member list views with filters

---

#### F2.4: Blackout Dates & Recurring Shifts
**Priority**: P1 (Operational efficiency)

**Description**: Advanced scheduling features for Ops Manager.

**Capabilities**:
- **Blackout date ranges** (airfield closed, no shifts needed)
- **Recurring shift patterns** (e.g., every Saturday, every first Monday)
- **Bulk shift creation** (create entire month of shifts in one action)
- **Shift templates** (save common configurations)

**User Stories**:
- "As Ops Manager, I want to mark Christmas week as closed"
- "As Ops Manager, I want to create Saturdays for 3 months in one go"
- "As Ops Manager, I want to save my 'typical weekend' shift pattern"

**Technical Implementation**:
- `blackoutDates` collection (already in Phase 1 schema)
- `shiftTemplates` collection
- Bulk creation Cloud Functions

---

### Success Criteria (Phase 2)

**Operational**:
- [ ] Zero coverage gaps go unnoticed (100% alert accuracy)
- [ ] Ops Manager spends <20 mins/day on volunteer management (down from 30)
- [ ] 25+ members indicate interest in Fire Crew (validation for Phase 3)
- [ ] Membership renewal reminders reduce manual admin by 50%

**Technical**:
- [ ] Advanced alerting Cloud Functions run reliably (>99% success rate)
- [ ] Bulk email operations complete in <5 minutes
- [ ] Member filters return results in <500ms
- [ ] System still operates within Firebase free tier

---

## Phase 3: Fire Crew Launch & Multi-Role Validation
**Timeline**: Q1 2026 (3-4 months post-Phase 2)  
**Development Effort**: 30-40 hours  
**Operational Cost**: £0-10/month

### Goals
1. Launch Fire Crew as second volunteer role
2. Validate multi-role system architecture
3. Prove scalability for future roles (Maintenance, Events, etc.)

---

### Features

#### F3.1: Fire Crew Role Implementation
**Priority**: P0 (Committed to club)

**Description**: Full implementation of Fire Crew volunteer role with aviation-specific requirements.

**Fire Crew Training Modules** (6 modules):
1. Fire Safety Basics
2. Emergency Response Procedures
3. Fire Equipment Operation
4. First Aid & CPR
5. Radio Communication
6. Advanced Firefighting Techniques (optional)

**Shift Types**:
- **Weekend On-Call** (Saturday/Sunday, 8am-8pm)
- **Weekday Evening On-Call** (Mon-Fri, 5pm-9pm)
- **Event Coverage** (Airshows, open days - variable hours)

**Unique Requirements**:
- Minimum 2 Fire Crew per weekend shift
- Maximum 2 consecutive weekends per volunteer (prevent burnout)
- 48-hour minimum booking notice (training coordination)
- Emergency contact required for all Fire Crew

**User Stories**:
- "As member, I want to volunteer for Fire Crew shifts"
- "As Fire Crew, I want on-call shifts that fit my schedule"
- "As Ops Manager, I want to ensure Fire Crew coverage every weekend"

**Technical Implementation**:
- Create Fire Crew `volunteerRole` configuration
- New shift types for on-call patterns
- Enhanced booking rules (min 2 per shift, max consecutive)
- Emergency contact field in user profiles

---

#### F3.2: Multi-Role Member Support
**Priority**: P0 (Required for dual-role volunteers)

**Description**: Enable members to volunteer across multiple roles simultaneously.

**Capabilities**:
- **Role switching** in member dashboard (toggle between Duty Pilot/Fire Crew views)
- **Combined calendar view** showing all volunteer commitments
- **Cross-role conflict detection** (can't be on Fire Crew and Duty Pilot same time)
- **Per-role training status** display
- **Per-role shift history** and statistics

**User Stories**:
- "As member trained in both roles, I want to see all my shifts in one place"
- "As system, I need to prevent double-booking across roles"
- "As member, I want separate training status for each role"

**Technical Implementation**:
- UI role selector component (already in Phase 1)
- Conflict detection in booking Cloud Functions
- Aggregated calendar queries across roles

---

#### F3.3: Role-Specific Reporting
**Priority**: P1 (Operational insight)

**Description**: Enhanced reporting breaking down by volunteer role.

**Reports**:
- **Coverage by Role** (Duty Pilot 85%, Fire Crew 90%)
- **Member Activity by Role** (Sarah: 10 Duty Pilot shifts, 5 Fire Crew shifts)
- **Training Progress by Role** (15 fully trained Duty Pilot, 8 fully trained Fire Crew)
- **Cross-Role Participation** (12 members active in both roles)
- **Role Launch Success** (Fire Crew timeline, coverage trends)

**User Stories**:
- "As Ops Manager, I want to compare coverage rates between roles"
- "As Committee, I need to see if Fire Crew launch was successful"
- "As Ops Manager, I want to identify volunteers doing both roles"

**Technical Implementation**:
- Enhanced reporting Cloud Functions
- Data aggregation across roles
- Comparative visualizations

---

### Success Criteria (Phase 3)

**Operational**:
- [ ] Fire Crew role live with 8+ fully trained volunteers
- [ ] 80%+ Fire Crew shift coverage achieved
- [ ] Zero double-bookings (members scheduled for 2 roles simultaneously)
- [ ] Ops Manager manages 2 roles in same time as previous 1 role

**Technical**:
- [ ] System handles 2 active roles without performance degradation
- [ ] Conflict detection works 100% reliably
- [ ] Member dashboard loads in <1 second with 2 roles
- [ ] All Phase 1 functionality still works perfectly

**Strategic**:
- [ ] Committee approves expansion to 3rd role (Maintenance)
- [ ] Multi-role architecture validated for future expansion
- [ ] Member satisfaction maintained (NPS >50)

---

## Phase 4: Aircraft Booking Integration
**Timeline**: Q2-Q3 2026 (6-9 months post-launch)  
**Development Effort**: 60-80 hours  
**Operational Cost**: £5-15/month

### Goals
1. Enable online aircraft booking (replacing paper logbook system)
2. Integrate volunteer shifts with aircraft operations
3. Prevent scheduling conflicts (can't fly and duty pilot simultaneously)
4. Provide unified operational view for Ops Manager

---

### Features

#### F4.1: Aircraft Management
**Priority**: P0 (Core booking functionality)

**Description**: Centralized aircraft resource management.

**Aircraft Database**:
- Aircraft registration, type, model
- Hourly rate (wet/dry)
- Availability status (Available, Maintenance, Grounded)
- Maintenance schedule and expiry dates
- Insurance requirements (pilot qualifications)
- Maximum booking duration (e.g., 3 hours for training aircraft)

**Capabilities**:
- **Aircraft catalog** with photos, specs, rates
- **Availability calendar** per aircraft (real-time)
- **Maintenance tracking** (next due, serviceability)
- **Usage statistics** (hours flown, utilization %)

**User Stories**:
- "As member, I want to see which aircraft are available on Saturday"
- "As Ops Manager, I want to mark aircraft as unavailable for maintenance"
- "As Committee, I want utilization reports per aircraft"

---

#### F4.2: Member Booking System
**Priority**: P0 (Core booking functionality)

**Description**: Online booking interface for members to reserve aircraft.

**Booking Flow**:
1. Select date and time
2. View available aircraft
3. Check eligibility (licence type, checkout status)
4. Book aircraft (instant or pending approval)
5. Receive confirmation email
6. Pre-flight reminders (24 hours before)

**Booking Rules**:
- **Minimum booking**: 1 hour
- **Maximum advance booking**: 14 days (configurable)
- **Cancellation policy**: Free >24 hours, £10 fee <24 hours
- **Conflict prevention**: Can't book if on volunteer shift same time
- **Instructor pairing**: Option to request instructor

**User Stories**:
- "As PPL holder, I want to book G-ABCD for Saturday 10am-12pm"
- "As student, I want to see which aircraft I'm checked out on"
- "As system, I need to prevent me booking a flight when I'm on duty pilot"

**Technical Implementation**:
- `aircraft` collection
- `aircraftBookings` collection
- Conflict detection Cloud Functions (check volunteer shifts)
- Booking approval workflow (optional, based on member status)

---

#### F4.3: Integrated Operations Dashboard
**Priority**: P1 (Ops Manager efficiency)

**Description**: Unified view of airfield operations - volunteers + aircraft.

**Dashboard Panels**:
- **Today's Schedule**: Who's duty pilot, who's flying what aircraft
- **Real-Time Status**: Aircraft on ground, in flight (future: flight tracker integration)
- **Upcoming Conflicts**: Warnings about potential double-bookings
- **Resource Utilization**: Volunteer coverage + aircraft booking rate
- **Weather Integration**: METAR/TAF display (future)

**Capabilities**:
- **Timeline view**: Hour-by-hour schedule of aircraft and volunteers
- **Resource view**: Per-aircraft and per-volunteer schedules
- **Conflict alerts**: Highlight scheduling issues
- **Quick actions**: Assign volunteer, cancel booking, contact member

**User Stories**:
- "As Ops Manager, I want to see the entire day's schedule at a glance"
- "As Ops Manager, I want to know if Sarah is trying to fly while on duty"
- "As Ops Manager, I want to contact all people flying today"

---

#### F4.4: Instructor Scheduling (Basic)
**Priority**: P2 (Nice to have)

**Description**: Basic instructor availability and pairing with students.

**Capabilities**:
- **Instructor availability calendar** (instructors mark available times)
- **Student pairing requests** (students can request specific instructor)
- **Dual bookings** (student + instructor + aircraft in one booking)
- **Instructor dashboard** (see all student bookings)

**User Stories**:
- "As instructor, I want to mark my availability for the week"
- "As student, I want to book aircraft + request my instructor"
- "As instructor, I want to see all my upcoming lessons"

**Technical Implementation**:
- `instructorAvailability` collection
- Enhanced booking flow for dual bookings
- Instructor-student pairing logic

---

### Success Criteria (Phase 4)

**Operational**:
- [ ] 50%+ members use online booking (vs. paper logbook)
- [ ] Zero double-bookings (member flying + volunteering simultaneously)
- [ ] Aircraft utilization increases 10%+ (easier booking = more flying)
- [ ] Ops Manager has single operational dashboard (not multiple systems)

**Technical**:
- [ ] Booking system 99.5%+ reliability
- [ ] Conflict detection 100% accurate
- [ ] Real-time availability updates (<3 seconds)
- [ ] System handles 50+ bookings per week

**Member Experience**:
- [ ] Members prefer online booking over paper (survey)
- [ ] Booking flow takes <2 minutes (target: <90 seconds)
- [ ] Confirmation emails received within 5 minutes
- [ ] Member NPS >55

---

## Phase 5: Payments & Billing Integration
**Timeline**: Q3-Q4 2026 (12-15 months post-launch)  
**Development Effort**: 80-100 hours  
**Operational Cost**: £10-20/month + Stripe fees (2.9% + 30p)

### Goals
1. Enable online membership payments
2. Automate flying fee billing
3. Reduce payment administration time by 50%+
4. Improve cash flow through easier payment options

---

### Features

#### F5.1: Stripe Payment Integration
**Priority**: P0 (Core payments)

**Description**: Secure payment processing via Stripe (Firebase Extension).

**Payment Methods Supported**:
- Credit/debit cards (Visa, Mastercard, Amex)
- Apple Pay / Google Pay
- UK bank account (Direct Debit - future)

**Capabilities**:
- **One-time payments** (membership, course fees)
- **Recurring payments** (annual membership auto-renewal)
- **Payment intents** (hold card authorization)
- **Refunds** (full or partial)
- **Payment history** (member view + admin view)

**Security**:
- PCI DSS compliant (Stripe handles card data)
- 3D Secure authentication
- Fraud detection (Stripe Radar)
- No card details stored in Firebase

**Technical Implementation**:
- Firebase Extension: stripe-firebase-extensions
- `payments` collection
- `paymentMethods` collection (tokenized)
- Cloud Functions for payment processing

---

#### F5.2: Membership Payment Processing
**Priority**: P0 (Revenue critical)

**Description**: Online membership fee payment and renewal.

**Membership Tiers**:
- **Full Member**: £XXX/year
- **Student Member**: £XXX/year
- **Social Member**: £XXX/year
- **Family Membership**: £XXX/year

**Capabilities**:
- **New membership payment** (during registration)
- **Renewal payment** (automated reminders 30/14/7 days before expiry)
- **Auto-renewal option** (opt-in recurring payment)
- **Payment plans** (monthly installments - future)
- **Member portal** (view payment history, receipts)

**User Stories**:
- "As new member, I want to pay my membership online during registration"
- "As member, I want automatic renewal reminders with payment link"
- "As member, I want to set up auto-renewal so I don't forget"
- "As Committee, I want to see outstanding membership payments"

---

#### F5.3: Flying Fee Billing
**Priority**: P1 (Post-flight process)

**Description**: Billing for aircraft usage based on flight time.

**Billing Flow**:
1. Member completes flight (logs hours in system)
2. System calculates fee (hours × aircraft rate)
3. Invoice generated automatically
4. Member receives email with payment link
5. Member pays online (card or saved payment method)
6. Receipt emailed, account credited

**Capabilities**:
- **Automatic invoicing** (post-flight)
- **Bulk charging** (charge all outstanding invoices monthly)
- **Payment reminders** (7/14/30 days overdue)
- **Account balance view** (member dashboard)
- **Saved payment methods** (pay with one click)

**User Stories**:
- "As member, I want to pay for my flight immediately after landing"
- "As member, I want to see my account balance and pay all at once"
- "As Ops Manager, I want to send payment reminders to overdue accounts"

---

#### F5.4: Course & Training Payments
**Priority**: P2 (Additional revenue)

**Description**: Online payment for training courses, checkouts, ratings.

**Course Types**:
- PPL training courses
- Differences training (new aircraft type)
- Night rating
- Aerobatic training
- Annual checkouts

**Capabilities**:
- **Course catalog** with prices and descriptions
- **Online enrollment** with instant payment
- **Deposit options** (pay £X now, balance later)
- **Payment schedules** (installments for expensive courses)

**User Stories**:
- "As student, I want to enroll in PPL course and pay deposit online"
- "As member, I want to book checkout flight and pay immediately"
- "As instructor, I want students to pay for lessons in advance"

---

#### F5.5: Financial Reporting
**Priority**: P1 (Committee oversight)

**Description**: Financial dashboards and reports for committee.

**Reports**:
- **Revenue by Source** (membership, flying fees, courses)
- **Outstanding Payments** (who owes what)
- **Payment Trends** (monthly revenue, YoY comparison)
- **Member Account Status** (paid up, overdue, credit balance)
- **Stripe Fees Summary** (total transaction costs)
- **Reconciliation Report** (match payments to bank statements)

**User Stories**:
- "As Treasurer, I want monthly revenue breakdown by category"
- "As Committee, I want to see YoY membership revenue growth"
- "As Ops Manager, I want list of overdue accounts for follow-up"

**Technical Implementation**:
- Stripe webhooks for payment events
- `invoices` collection
- `transactions` collection
- Reporting Cloud Functions with aggregation

---

### Success Criteria (Phase 5)

**Financial**:
- [ ] 70%+ membership renewals paid online
- [ ] Payment processing admin time reduced 50%+
- [ ] Outstanding payment balance reduced 30%+
- [ ] Stripe fees <3% of revenue

**Operational**:
- [ ] Payment processing 99.5%+ success rate
- [ ] Automated invoicing works reliably (100% accuracy)
- [ ] Member payment history accurate and accessible
- [ ] Committee has real-time financial dashboards

**Member Experience**:
- [ ] Members find online payment easier than previous method (survey)
- [ ] Payment flow takes <2 minutes
- [ ] Receipts emailed within 5 minutes
- [ ] Member NPS >60

---

## Phase 6+: Complete Member Platform
**Timeline**: 2027-2030 (Ongoing)  
**Development Effort**: 400-600 hours over 3 years  
**Operational Cost**: £20-40/month

### Vision
Transform into complete member lifecycle platform with all operational needs integrated.

---

### F6.1: Document Management
**Timeline**: Q1 2027 | **Effort**: 40-60 hours

**Description**: Digital storage for member and operational documents.

**Document Types**:
- Member insurance certificates
- Medical certificates (pilots)
- Pilot licences and ratings
- Aircraft documents (permits, insurance, maintenance records)
- Club policies and procedures
- Safety bulletins
- Meeting minutes

**Capabilities**:
- **Upload and storage** (Firebase Storage)
- **Document expiry tracking** (automatic reminders)
- **Version control** (keep document history)
- **Access control** (some docs public, some member-only, some committee-only)
- **Search and categorization**
- **Automatic OCR** (search within PDFs)

**User Stories**:
- "As member, I want to upload my medical certificate and get reminded before expiry"
- "As Ops Manager, I want to access aircraft insurance documents quickly"
- "As new member, I want to read club policies in one place"

---

### F6.2: Digital Flight Logging
**Timeline**: Q2 2027 | **Effort**: 60-80 hours

**Description**: Digital logbook integrated with aircraft bookings.

**Capabilities**:
- **Automatic log entries** from aircraft bookings
- **Manual log entry** for external flights
- **Totals calculation** (total hours, PIC hours, dual hours)
- **Currency tracking** (90-day, landings, night, etc.)
- **Ratings and endorsements** tracking
- **Export to CSV** (for CAA, insurance)
- **Logbook statistics** (hours per year, aircraft types)

**User Stories**:
- "As pilot, my flight automatically appears in my logbook after booking"
- "As pilot, I want to track my currency for different operations"
- "As pilot, I need to export my logbook for insurance"

**Technical Implementation**:
- `flightLogs` collection
- Auto-population from `aircraftBookings`
- Currency calculation Cloud Functions
- Integration with CAA requirements

---

### F6.3: Maintenance Tracking
**Timeline**: Q3 2027 | **Effort**: 50-70 hours

**Description**: Aircraft maintenance and airworthiness tracking.

**Capabilities**:
- **Maintenance schedule** (50hr, 100hr, annual)
- **Defect logging** (pilot reports issues)
- **Rectification tracking** (when fixed, by whom)
- **Airworthiness status** (serviceable, unserviceable, limited)
- **Automated grounding** (aircraft auto-removed from booking when unserviceable)
- **Maintenance history** (full aircraft lifecycle)

**User Stories**:
- "As pilot, I want to report a defect after my flight"
- "As engineer, I want to see all outstanding defects"
- "As Ops Manager, I want aircraft to be unbookable when unserviceable"

---

### F6.4: Event Management
**Timeline**: Q4 2027 | **Effort**: 40-50 hours

**Description**: Organize and manage club events (airshows, fly-ins, social events).

**Capabilities**:
- **Event creation** (date, location, description)
- **Volunteer signup** (event-specific roles)
- **Attendee registration** (RSVP tracking)
- **Ticket sales** (if applicable, via Stripe)
- **Event communications** (announcements, reminders)
- **Post-event feedback** (surveys)

**User Stories**:
- "As Committee, I want to create an open day event and recruit volunteers"
- "As member, I want to RSVP for the summer BBQ"
- "As volunteer coordinator, I want to see who signed up for each role"

---

### F6.5: Mobile Apps (iOS & Android)
**Timeline**: 2028 | **Effort**: 200-300 hours

**Description**: Native mobile apps for iOS and Android.

**Why Mobile Apps?**
- Push notifications (shift reminders, urgent coverage needs)
- Offline access (view schedule without internet)
- Better user experience (native feel vs. mobile web)
- Quick actions (book shift in 2 taps)
- Calendar integration (sync shifts to phone calendar)

**Capabilities**:
- All Phase 1-5 features available in app
- Push notifications
- Offline mode (view booked shifts)
- Face ID / Touch ID login
- Quick booking shortcuts
- Widget (today's schedule on home screen)

**Technical Stack**:
- React Native (code sharing with web app)
- Firebase SDKs (iOS/Android)
- Apple App Store + Google Play Store

---

### F6.6: Advanced Analytics & Insights
**Timeline**: 2029 | **Effort**: 60-80 hours

**Description**: Predictive analytics and operational intelligence.

**Capabilities**:
- **Predictive coverage needs** (ML model predicts when gaps likely)
- **Member engagement scoring** (identify at-risk members)
- **Utilization optimization** (suggest best times to offer incentives)
- **Seasonal trends** (when is demand highest?)
- **Volunteer burnout detection** (flag over-committed members)
- **Revenue forecasting** (predict next quarter's income)

**User Stories**:
- "As Ops Manager, I want to know which weekends will be hard to fill"
- "As Committee, I want to identify members at risk of lapsing"
- "As Treasurer, I want accurate revenue forecasts for budgeting"

**Technical Implementation**:
- BigQuery (data warehouse)
- TensorFlow (ML models)
- Looker Studio (dashboards)

---

## Technology Evolution

### Current Stack (Phase 1-3)
```
Frontend: React + Tailwind
Backend: Firebase (Firestore, Functions, Auth, Hosting)
Email: SendGrid
```

### Added Layers (Phase 4-5)
```
+ Payments: Stripe
+ Storage: Firebase Storage
+ Search: Algolia (if needed)
```

### Future Considerations (Phase 6+)
```
+ Mobile: React Native
+ Analytics: BigQuery + TensorFlow
+ API: Cloud Run (if heavy custom logic needed)
+ Real-time: Firebase Realtime Database (for flight tracking)
```

---

## Prioritization Framework

### How We Decide What to Build Next

**1. Business Value**
- Does it solve a painful operational problem?
- Does it generate revenue or reduce costs?
- Do members/committee actively request it?

**2. Technical Feasibility**
- Can we build it with current tech stack?
- Are there existing solutions to integrate?
- What's the risk of technical debt?

**3. Member Demand**
- How many members would use it?
- Is there proven demand (surveys, requests)?
- Would it improve member satisfaction?

**4. Resource Availability**
- Do we have time/budget to build well?
- Can we maintain it long-term?
- Are dependencies ready (other features, data)?

**5. Strategic Fit**
- Does it align with 5-year vision?
- Does it enable future features?
- Does it differentiate us from other clubs?

---

## Decision Gates Between Phases

### Phase 1 → Phase 2 (GO/NO-GO)
**Review at 3 months post-launch**

**GO Criteria** (must meet all):
- [ ] 60%+ active members registered
- [ ] 80%+ duty pilot shift coverage
- [ ] <5% cancellation rate
- [ ] Zero coverage gaps unnoticed
- [ ] Member NPS >40
- [ ] System stable (no critical bugs)

**If NO-GO**: Fix issues, extend Phase 1, reassess in 1 month

---

### Phase 3 → Phase 4 (GO/NO-GO)
**Review 3 months after Fire Crew launch**

**GO Criteria**:
- [ ] Fire Crew has 80%+ coverage
- [ ] 2 roles coexist without issues
- [ ] System performance not degraded
- [ ] Committee approves aircraft booking priority
- [ ] Member satisfaction maintained (NPS >50)

**If NO-GO**: Add 3rd role (Maintenance) before aircraft booking

---

### Phase 4 → Phase 5 (GO/NO-GO)
**Review 3 months after aircraft booking launch**

**GO Criteria**:
- [ ] 50%+ members use online booking
- [ ] Zero critical booking conflicts
- [ ] Aircraft utilization increased or stable
- [ ] Committee approves online payment implementation
- [ ] Stripe account and bank verification complete

**If NO-GO**: Optimize booking system, delay payments

---

## Alternative Scenarios

### Scenario A: Faster Growth
**If membership grows >20% year-over-year**

**Implications**:
- Accelerate Phase 4 (aircraft booking) to handle demand
- Prioritize scalability optimizations
- Consider dedicated staff for admin
- Increase Firebase budget

**Adjustments**:
- Hire part-time developer for Phase 6 features
- Add Phase 7: Second location support (if club expands)

---

### Scenario B: Budget Constraints
**If operational costs exceed £30/month**

**Implications**:
- Delay non-essential features (analytics, mobile apps)
- Optimize queries and storage
- Consider partial migration (move static content to cheaper hosting)

**Adjustments**:
- Focus on cost-saving features (automation → reduce staff time)
- Delay Phase 6 until finances improve

---

### Scenario C: Integration Opportunity
**If external system partnership available (e.g., aviation booking platform)**

**Implications**:
- Evaluate build vs. integrate for aircraft booking
- Potential API integration instead of custom build
- Could accelerate timeline or reduce development effort

**Adjustments**:
- Phase 4 becomes integration project instead of full build
- Reallocate saved time to other features

---

## Risks to Roadmap

| Risk | Probability | Impact | Mitigation |
|------|------------|--------|------------|
| **Phase 1 doesn't validate** | Low | Critical | Thorough beta testing, tight scope |
| **Committee priorities shift** | Medium | High | Regular stakeholder alignment, show ROI |
| **Firebase costs spiral** | Low | Medium | Monitoring, optimization, migration plan |
| **Developer burnout** (volunteer) | Medium | High | Realistic timelines, celebrate wins, breaks |
| **Competing systems introduced** | Low | Medium | Demonstrate value early, lock in Phase 1 |
| **Member resistance to change** | Medium | Medium | Training, communication, phased rollout |
| **Technical debt accumulates** | Medium | High | Refactoring time between phases, code reviews |

---

## Success Metrics (3-5 Year Horizon)

### Operational Excellence
- [ ] Ops Manager admin time reduced 50%+ (from pre-system baseline)
- [ ] 90%+ shift coverage across 5+ volunteer roles
- [ ] 80%+ aircraft bookings online
- [ ] 95%+ payment success rate
- [ ] Zero critical operational failures

### Member Engagement
- [ ] 90%+ active members use platform weekly
- [ ] Member NPS >60
- [ ] 70%+ members participate in volunteering
- [ ] 50%+ members have multiple volunteer roles
- [ ] Membership retention improved 10%+

### Financial Health
- [ ] Online payments represent 80%+ of revenue
- [ ] Outstanding payment balance reduced 50%+
- [ ] Platform operational cost <£50/month
- [ ] ROI positive (time saved × hourly rate > total cost)

### Platform Maturity
- [ ] 6+ integrated modules operational
- [ ] Mobile apps launched (iOS + Android)
- [ ] System supports 500+ members, 1000+ transactions/month
- [ ] <5 hours/month maintenance required
- [ ] Uptime >99.5%

---

## Conclusion

This roadmap provides a **clear path from MVP to comprehensive platform** over 3-5 years. The phased approach enables:

✅ **Incremental validation** - Prove each phase before investing in next  
✅ **Manageable scope** - Avoid overwhelming users and developers  
✅ **Flexibility** - Adjust priorities based on feedback and changing needs  
✅ **Sustainability** - Keep costs proportional to value delivered  
✅ **Strategic vision** - Build toward complete member platform  

**Next Steps**: Focus on Phase 1 success, then revisit this roadmap at each decision gate.

---

*Document Version: 1.0*  
*Last Updated: October 1, 2025*  
*Part of: Herefordshire Aeroclub Member Platform Specification*