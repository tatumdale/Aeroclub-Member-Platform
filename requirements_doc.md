# Requirements Specification
## Herefordshire Aeroclub Volunteer Management System - Phase 1

---

## Document Overview

**Scope**: Phase 1 - Volunteer Management (Duty Pilot Focus)  
**Timeline**: 6-8 weeks development  
**Priority System**: P0 (Must Have), P1 (Should Have), P2 (Nice to Have)

---

## Functional Requirements

### FR-1: Public Calendar View
**Priority**: P0 (MVP Critical)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR-1.1 | Display public calendar showing duty pilot shift needs for next 3 months | Calendar loads in <2 seconds, shows all open and filled shifts |
| FR-1.2 | Show three shift types: Morning (8:30am-1pm), Afternoon (1pm-5:30pm), Full Day (8:30am-5:30pm) | Each shift clearly labeled with type and time range |
| FR-1.3 | Visual status indicators: Available (green), Filled (grey), Pending Approval (amber), Backup Available (blue outline) | Color-blind safe palette, distinct visual indicators |
| FR-1.4 | Display shift status text: "Open - X volunteers needed", "Full", "Pending" | Status updates in real-time when bookings change |
| FR-1.5 | Show blackout dates (airfield closed) clearly with no bookable shifts | Blackout dates displayed with reason (e.g., "Airfield Closed") |
| FR-1.6 | "Login to Volunteer" button visible on all open shifts | Clicking button redirects unauthenticated users to login page |
| FR-1.7 | Mobile responsive - calendar adapts to phone screens (list view on mobile) | Calendar usable on screens from 320px width upwards |
| FR-1.8 | Role selector showing "Duty Pilot" (active) and future roles (greyed) | Dropdown/pills show current and coming soon roles |
| FR-1.9 | Footer note about future volunteer opportunities | Text: "More volunteer opportunities coming soon - Fire Crew, Maintenance, and more!" |

---

### FR-2: Member Authentication & Profile
**Priority**: P0 (MVP Critical)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR-2.1 | Email/password registration and login | Users can create account with email verification (optional Phase 1) |
| FR-2.2 | "Forgot password" flow via email reset link | Password reset link sent within 5 minutes, valid for 1 hour |
| FR-2.3 | Profile fields: Full Name, Email, Phone Number, Availability Preferences, Member Since | All fields except Availability Preferences required |
| FR-2.4 | "Your Volunteer Roles" section showing active roles and interested roles | Display Duty Pilot status, checkboxes for future role interests |
| FR-2.5 | Training status display (read-only for members): Till System, Phone Management, Visitor Check-in, Aircraft Logs, Pilot Support | Each module shows trained/untrained status with date and trainer name |
| FR-2.6 | "Interested in future roles?" multi-select: Fire Crew, Maintenance, Events, Instructing | Checkbox selection saved to user profile |
| FR-2.7 | View own upcoming shifts with role indicator (Duty Pilot badge/icon) | List of upcoming shifts sorted by date |
| FR-2.8 | Shift history with role filter | Paginated list showing past 50 shifts, filterable by role |
| FR-2.9 | Profile edit capability (except training status which is read-only) | Members can update name, phone, availability preferences |

---

### FR-3: Shift Booking & Cancellation
**Priority**: P0 (MVP Critical)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR-3.1 | Members can book available Duty Pilot shifts (max 2 volunteers per shift) | Booking button disabled when shift full |
| FR-3.2 | Shift details show role badge: "Duty Pilot" with icon | Role clearly identified on booking confirmation |
| FR-3.3 | If member fully trained AND vacancy exists → Auto-approve + confirmation email | Booking status set to "approved", email sent within 5 minutes |
| FR-3.4 | If member not fully trained OR shift full → Pending approval + notification to Ops Manager | Booking status "pending", Ops Manager notified within 5 minutes |
| FR-3.5 | Members can cancel shifts at any time via system | Cancel button available on all future shifts |
| FR-3.6 | Warning message on cancellation: "If cancelling within 3 days of shift, please also call the office on [phone]" | Warning displayed in modal before cancellation confirmed |
| FR-3.7 | Cancellation triggers notification to Ops Manager | Email sent to Ops Manager within 5 minutes |
| FR-3.8 | Members can opt-in as "Backup" for Duty Pilot shifts | Backup status displayed separately from committed bookings |
| FR-3.9 | "Interested in other roles?" prompt after first successful booking | Shown once per user, dismissible |

---

### FR-4: Operations Manager Dashboard
**Priority**: P0 (MVP Critical)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR-4.1 | Sidebar navigation: Dashboard, Duty Pilot Shifts, Manage Roles, Members, Reports, Settings | All menu items accessible, active state highlighted |
| FR-4.2 | "Manage Roles" page shows list of roles with status (Active: Duty Pilot, Coming Soon: others) | Duty Pilot card shows full details, others show "Coming Soon" badge |
| FR-4.3 | Duty Pilot role card displays: Active status, 5 training modules, 3 shift types, auto-approve rules | All configuration visible, "Edit" button greyed with "Coming Q1 2026" tooltip |
| FR-4.4 | "Create New Role" button greyed with tooltip | Tooltip: "Role creation coming Q1 2026 - track interested members now!" |
| FR-4.5 | Calendar view: All Duty Pilot shifts with status indicators | Same view as public calendar with additional admin controls |
| FR-4.6 | Role filter on calendar (currently only Duty Pilot active) | Dropdown shows Duty Pilot (clickable), others greyed |
| FR-4.7 | "Upcoming Uncovered Shifts" panel showing all open Duty Pilot shifts | Sorted by date, shows days until shift, volunteers needed count |
| FR-4.8 | "Pending Approvals" panel with member names, training status, approve/reject buttons | Each pending booking shows member name, shift details, training completion status |
| FR-4.9 | Approve/Reject buttons with optional note to member | Note field optional, character limit 500 |
| FR-4.10 | Create Duty Pilot shift needs: Date, Shift Type, Number of Volunteers Needed (1-2) | Form with date picker, dropdown for shift type, number selector |
| FR-4.11 | Edit/Delete shift needs with warning if volunteers already booked | Warning modal: "X members are booked for this shift. They will be notified of changes." |
| FR-4.12 | Set blackout dates (date range, reason) | Date range picker, reason text field (required) |
| FR-4.13 | Manually assign members to Duty Pilot shifts (overrides auto-approval) | Member search, assign button, confirmation email sent |

---

### FR-5: Member Management (Ops Manager)
**Priority**: P0 (MVP Critical)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR-5.1 | View all registered members in searchable table | Search by name/email, results update in real-time |
| FR-5.2 | Table columns: Name, Email, Active Role (Duty Pilot badge if trained), Interested Roles, Total Shifts, Last Active | Sortable by any column |
| FR-5.3 | Filter by: Training Status, Activity Level, Availability Preferences, Role Interest | Multiple filters can be applied simultaneously |
| FR-5.4 | "Future Role Interest" column shows member-selected interests with icons | Icons for Fire Crew, Maintenance, etc. |
| FR-5.5 | Export member list with role interests for planning | CSV export with all visible columns |
| FR-5.6 | Edit member profiles including notes field (Ops Manager only) | All profile fields editable, notes field character limit 2000 |
| FR-5.7 | Update Duty Pilot training: Check/uncheck modules, add "Trained By" and "Date Trained" | Each module has checkbox, trainer dropdown (all ops managers), date picker |
| FR-5.8 | View member shift history filtered by role | Shows all past and upcoming shifts, filterable and sortable |
| FR-5.9 | Member detail view shows "Volunteer Profile Summary" with role participation | Summary includes: total shifts, cancellation rate, training status, role interests |

---

### FR-6: Notifications & Alerts
**Priority**: P0 (MVP Critical)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR-6.1 | Member books Duty Pilot shift → Confirmation email (auto-approved or pending) | Email sent within 5 minutes, includes shift details and next steps |
| FR-6.2 | Approval granted → Email to member | Email sent within 5 minutes of approval action |
| FR-6.3 | Approval rejected → Email to member with reason (if provided) | Email includes optional rejection reason from Ops Manager |
| FR-6.4 | 3 days before Duty Pilot shift → Reminder email to assigned member | Automated email sent at 8am, 3 days prior to shift |
| FR-6.5 | 24 hours before shift → Final reminder email | Automated email sent at 8am, 1 day prior to shift |
| FR-6.6 | Member cancels → Email to Ops Manager | Email sent within 5 minutes with member name, shift details, cancellation time |
| FR-6.7 | Member books pending shift → Email to Ops Manager | Email sent within 5 minutes with link to approve/reject |
| FR-6.8 | **CRITICAL ALERT**: If shift within 3 days has no coverage → Email to all Ops Managers | Daily automated check at 8am, email lists all uncovered shifts |
| FR-6.9 | Email templates include role context (e.g., "Your Duty Pilot shift on...") | All emails clearly identify the volunteer role |

---

### FR-7: Reporting & Analytics
**Priority**: P1 (Should Have - Post-MVP)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR-7.1 | Member Activity Report: List of members, total shifts by role, shifts by month, last shift date | Exportable to Excel, filterable by date range |
| FR-7.2 | Coverage Report (per role): % of shifts covered, average time to fill, cancellation rate | Updated daily, shows trends over time |
| FR-7.3 | Training Overview (per role): Members by training status (fully trained, partially, untrained) | Visual charts, drill-down to member details |
| FR-7.4 | **Role Interest Report**: Members interested in future roles (Fire Crew: X, Maintenance: Y) | Shows member names, contact info, current activity level |
| FR-7.5 | Excel export: Shift schedule with role, status, assigned members, dates, training status | One-click export, formatted for printing |
| FR-7.6 | Future role planning report with recommendations | "You have X members interested in Fire Crew - ready to launch when needed" |
| FR-7.7 | Date range filtering on all reports | Standard date picker, defaults to last 30 days |

---

### FR-8: Role-Based Access Control
**Priority**: P0 (MVP Critical)

| Role | Access Rights | Details |
|------|---------------|---------|
| **Public (Unauthenticated)** | • View volunteer calendar (shifts, availability)<br>• View role selector (future roles greyed)<br>• Access login/register pages | Cannot book shifts or access any member data |
| **Member (Authenticated)** | • All public access<br>• Book Duty Pilot shifts<br>• Cancel own shifts<br>• View/edit own profile<br>• View own training status (read-only)<br>• Indicate interest in future roles<br>• View own shift history | Cannot view other members' data or access admin functions |
| **Operations Manager** (Max 3 users) | • All member access<br>• Manage all Duty Pilot shifts<br>• Approve/reject bookings<br>• Manage member profiles and training<br>• Create/edit shift needs<br>• View role framework (read-only)<br>• View all reports<br>• Manage blackout dates<br>• Manually assign members to shifts<br>• View all member profiles (including notes) | Full administrative access to volunteer management |
| **Committee** (Read-only) | • View all Duty Pilot shifts<br>• View all member profiles (except Ops Manager notes)<br>• View all reports<br>• View role framework | Cannot edit anything, oversight only |

---

### FR-9: Future Module Placeholders (UI Structure)
**Priority**: P0 (MVP - Navigation Framework)

| ID | Requirement | Acceptance Criteria |
|----|-------------|---------------------|
| FR-9.1 | Navigation sidebar includes greyed-out future modules with "Coming Soon" badges | Modules visible but disabled, tooltips explain when available |
| FR-9.2 | Member navigation includes: Home, Volunteer, [Bookings - Soon], [My Account - Soon], Profile, Logout | "Coming Soon" items greyed with lock icon |
| FR-9.3 | Ops Manager navigation includes: Dashboard, Volunteer Management, [Aircraft - Soon], [Members CRM - Soon], [Payments - Soon], Reports, Settings | Future modules visible but disabled |
| FR-9.4 | Clicking greyed items shows tooltip: "This feature is coming in [Phase X]. Current focus: Volunteer management" | Tooltip provides context and timeline |
| FR-9.5 | Footer includes: "Volunteer Management v1.0 - Part of the Herefordshire Aeroclub Member Platform" | Sets expectation of larger platform vision |

---

## Non-Functional Requirements

### NFR-1: Performance
**Priority**: P0 (MVP Critical)

| ID | Requirement | Target | Measurement |
|----|-------------|--------|-------------|
| NFR-1.1 | Page load time on 4G mobile connection | <2 seconds | Lighthouse, Chrome DevTools |
| NFR-1.2 | Calendar rendering for 3 months of data | <1 second | Custom performance trace |
| NFR-1.3 | Email delivery time from trigger event | <5 minutes | SendGrid analytics |
| NFR-1.4 | Real-time shift updates (when booking created/cancelled) | <3 seconds | Firebase Firestore latency |
| NFR-1.5 | Search results in member management | <500ms | Custom performance trace |
| NFR-1.6 | Initial bundle size (gzipped) | <200KB | Webpack Bundle Analyzer |

---

### NFR-2: Security
**Priority**: P0 (MVP Critical)

| ID | Requirement | Implementation |
|----|-------------|----------------|
| NFR-2.1 | HTTPS enforced on all pages | Firebase Hosting automatic SSL |
| NFR-2.2 | Password requirements: minimum 8 characters, 1 uppercase, 1 number | Firebase Auth configuration |
| NFR-2.3 | Session timeout after 30 days inactivity | Firebase Auth session management |
| NFR-2.4 | Role-based access controls enforced server-side | Firestore Security Rules |
| NFR-2.5 | GDPR compliant: Cookie consent, data export, account deletion | Built-in features, privacy policy |
| NFR-2.6 | Email addresses not exposed in client-side code | Server-side only via Cloud Functions |
| NFR-2.7 | Audit logging: All data modifications include createdBy, updatedBy, timestamps | Database schema enforcement |

---

### NFR-3: Availability & Reliability
**Priority**: P0 (MVP Critical)

| ID | Requirement | Target | Monitoring |
|----|-------------|--------|------------|
| NFR-3.1 | System uptime | 99% (Firebase SLA) | Firebase Status Dashboard |
| NFR-3.2 | Automated daily database backups | Daily at 2am UTC | Firebase automatic backups |
| NFR-3.3 | Recovery Time Objective (RTO) | <4 hours | Manual restore from backup |
| NFR-3.4 | Recovery Point Objective (RPO) | <24 hours | Daily backup frequency |
| NFR-3.5 | Email delivery success rate | >98% | SendGrid analytics |
| NFR-3.6 | Zero data loss on system failures | Guaranteed | Firebase transactional writes |

---

### NFR-4: Usability & Accessibility
**Priority**: P0 (MVP Critical)

| ID | Requirement | Standard | Validation |
|----|-------------|----------|------------|
| NFR-4.1 | Mobile responsive design (320px to 2560px) | Mobile-first approach | Manual testing on devices |
| NFR-4.2 | WCAG 2.1 Level AA compliance | Accessibility standard | WAVE, axe DevTools |
| NFR-4.3 | Keyboard navigation support (Tab, Enter, Escape) | All interactive elements | Manual testing |
| NFR-4.4 | Focus indicators visible on all interactive elements | 2px outline, high contrast | Visual inspection |
| NFR-4.5 | Color contrast ratio for text | ≥4.5:1 (normal text), ≥3:1 (large text) | Contrast checker tool |
| NFR-4.6 | Screen reader compatibility | NVDA, JAWS, VoiceOver | Manual testing |
| NFR-4.7 | Maximum 3 clicks to book a shift from homepage | User journey optimization | User testing |
| NFR-4.8 | Error messages clear and actionable | Plain language, suggest fixes | Content review |

---

### NFR-5: Scalability
**Priority**: P1 (Should Have)

| ID | Requirement | Target | Notes |
|----|-------------|--------|-------|
| NFR-5.1 | Support up to 500 registered members | Phase 1-3 target | Firebase handles easily |
| NFR-5.2 | Support up to 200 shifts per month | All volunteer roles | Indexed queries required |
| NFR-5.3 | Support up to 500 bookings per month | Peak load scenario | Within Firebase free tier |
| NFR-5.4 | Support 100 concurrent users | Peak time (Sunday morning) | Firebase auto-scales |
| NFR-5.5 | Database queries remain <500ms at scale | With proper indexing | Firestore composite indexes |
| NFR-5.6 | Email sending capacity: 2000/month | Year 2-3 estimate | SendGrid free tier: 3000/month |

---

### NFR-6: Maintainability
**Priority**: P1 (Should Have)

| ID | Requirement | Implementation |
|----|-------------|----------------|
| NFR-6.1 | Code documentation: All functions have JSDoc comments | Enforced in code review |
| NFR-6.2 | Component documentation: Storybook for all UI components | Phase 2 addition |
| NFR-6.3 | Database schema documentation: README in repository | Markdown documentation |
| NFR-6.4 | API documentation: All Cloud Functions documented | JSDoc + OpenAPI spec |
| NFR-6.5 | System requires <5 hours/month maintenance (post-launch) | Monitoring + automation |
| NFR-6.6 | Deployment process automated via CI/CD | GitHub Actions pipeline |

---

### NFR-7: Browser Support
**Priority**: P0 (MVP Critical)

| Browser | Minimum Version | Support Level | Notes |
|---------|----------------|---------------|-------|
| Chrome | Last 2 versions | Full support | Primary development browser |
| Firefox | Last 2 versions | Full support | Tested regularly |
| Safari | Last 2 versions | Full support | iOS Safari critical |
| Edge | Last 2 versions | Full support | Chromium-based |
| Mobile Safari | iOS 14+ | Full support | iPhone/iPad users |
| Chrome Mobile | Android 10+ | Full support | Android users |
| Internet Explorer 11 | N/A | ❌ Not supported | EOL browser |

---

## Data Requirements

### DR-1: User Data Storage
**Priority**: P0 (MVP Critical)

| Data Field | Type | Required | Validation | Privacy |
|------------|------|----------|------------|---------|
| User ID (UID) | String (Firebase Auth) | Yes | Auto-generated | Internal only |
| Email | String | Yes | Valid email format | PII - encrypted |
| Full Name | String | Yes | 2-100 characters | PII |
| Phone Number | String | Yes | UK format preferred | PII |
| Availability Preferences | Text | No | Max 500 characters | Internal |
| Member Since | Timestamp | Yes | Auto-set on creation | Public |
| Role | Enum | Yes | member, operations_manager, committee | Internal |
| Role Training | Object | Yes | Structured per role | Internal |
| Role Interests | Array | No | Valid role IDs | Internal |
| Ops Manager Notes | Text | No | Max 2000 characters | Ops Manager only |

---

### DR-2: Shift Data Storage
**Priority**: P0 (MVP Critical)

| Data Field | Type | Required | Validation |
|------------|------|----------|------------|
| Shift ID | String | Yes | Auto-generated |
| Role ID | String (Reference) | Yes | Valid role ID |
| Date | Timestamp | Yes | Future date only |
| Shift Type ID | String | Yes | morning, afternoon, full-day |
| Volunteers Needed | Number | Yes | 1-2 for Duty Pilot |
| Status | Enum | Yes | Computed: open, partial, filled |
| Created By | String (User ID) | Yes | Valid user ID |
| Created At | Timestamp | Yes | Auto-set |
| Updated At | Timestamp | Yes | Auto-update |

---

### DR-3: Booking Data Storage
**Priority**: P0 (MVP Critical)

| Data Field | Type | Required | Validation |
|------------|------|----------|------------|
| Booking ID | String | Yes | Auto-generated |
| Shift ID | String (Reference) | Yes | Valid shift ID |
| Role ID | String (Reference) | Yes | Valid role ID |
| User ID | String (Reference) | Yes | Valid user ID |
| Status | Enum | Yes | pending, approved, rejected, cancelled |
| Is Backup | Boolean | No | Default: false |
| Approved By | String (User ID) | No | Valid user ID (if approved) |
| Approved At | Timestamp | No | Set on approval |
| Rejection Reason | Text | No | Max 500 characters |
| Reminder Sent 3 Days | Boolean | No | Default: false |
| Reminder Sent 24 Hours | Boolean | No | Default: false |
| Created At | Timestamp | Yes | Auto-set |
| Updated At | Timestamp | Yes | Auto-update |
| Cancelled At | Timestamp | No | Set on cancellation |

---

### DR-4: Data Retention & Privacy
**Priority**: P0 (GDPR Compliance)

| Requirement | Policy | Implementation |
|-------------|--------|----------------|
| User account data | Retained while account active | User can delete account anytime |
| Deleted account data | Anonymized, not deleted | Convert to "Deleted User {ID}" |
| Booking history | Retained indefinitely for auditing | Required for operational records |
| Email notification logs | Retained for 90 days | Auto-delete via Cloud Function |
| Audit logs | Retained for 7 years | Compliance requirement |
| Data export request | Provided within 30 days | Manual export via Ops Manager |
| Right to be forgotten | Anonymize within 30 days | User ID retained, PII removed |

---

## Integration Requirements

### IR-1: Email System (SendGrid)
**Priority**: P0 (MVP Critical)

| Requirement | Specification |
|-------------|---------------|
| Integration Method | Firebase Extension: firestore-send-email |
| Email Provider | SendGrid (Free tier: 100 emails/day) |
| From Address | noreply@herefordshireaeroclub.co.uk |
| Reply-To Address | operations@herefordshireaeroclub.co.uk |
| Template Engine | SendGrid Dynamic Templates |
| Delivery Tracking | Yes - via SendGrid webhook |
| Bounce Handling | Automatic via SendGrid |
| Unsubscribe | Not required for transactional emails |

---

### IR-2: Future Integrations (Placeholders)
**Priority**: P2 (Future Phases)

| Integration | Phase | Purpose |
|-------------|-------|---------|
| Stripe Payments | Phase 5 | Membership fees, flying fees, course payments |
| Google Calendar | Phase 4 | Sync volunteer shifts to member calendars |
| SMS (Twilio) | Phase 3 | Urgent notifications for coverage gaps |
| CRM System | Phase 6 | Member data sync (TBD which CRM) |
| Weather API | Phase 6 | Flight operations integration |
| Aircraft Booking System | Phase 4 | Conflict detection with volunteer shifts |

---

## Validation Rules

### VR-1: Shift Booking Rules
**Priority**: P0 (MVP Critical)

| Rule | Validation |
|------|------------|
| Cannot book past shifts | Date must be >= today |
| Cannot book blackout dates | Check blackoutDates collection |
| Cannot exceed volunteer limit | Count approved bookings < volunteersNeeded |
| Cannot book same shift twice | Check existing bookings for user + shift |
| Cannot book overlapping shifts | Check user has no shift at same date/time |
| Training required for auto-approve | User must have all required training modules |

---

### VR-2: Training Update Rules
**Priority**: P0 (MVP Critical)

| Rule | Validation |
|------|------------|
| Only Ops Manager can update training | Role check in Firestore Rules |
| Training date cannot be future | Date <= today |
| Trained By must be valid Ops Manager | Cross-reference with user roles |
| All 5 modules required for "Fully Trained" | Boolean computed field |

---

### VR-3: Profile Update Rules
**Priority**: P0 (MVP Critical)

| Rule | Validation |
|------|------------|
| Email must be unique | Check existing users |
| Phone number format | UK format: +44 XXXX XXXXXX or 07XXX XXXXXX |
| Name minimum length | 2 characters |
| Availability preferences max length | 500 characters |
| Members cannot edit training status | UI disabled + Firestore Rules block |

---

## Error Handling Requirements

### EH-1: User-Facing Errors
**Priority**: P0 (MVP Critical)

| Error Scenario | User Message | Action |
|----------------|--------------|--------|
| Network connection lost | "Connection lost. Please check your internet and try again." | Retry button |
| Shift already full | "This shift is now full. Would you like to join as a backup volunteer?" | Backup option |
| Booking conflict | "You already have a shift at this time. Please choose a different shift." | Calendar view |
| Authentication expired | "Your session has expired. Please log in again." | Redirect to login |
| Permission denied | "You don't have permission to perform this action." | Contact support link |
| Email sending failed | "We couldn't send your confirmation email. Your booking is saved, but please check your spam folder." | Acknowledge button |

---

### EH-2: System Errors (Logged)
**Priority**: P0 (MVP Critical)

| Error Type | Logging | Alert |
|------------|---------|-------|
| Firestore write failure | Error log + context | Ops Manager email if critical |
| Cloud Function timeout | Error log + function name | Alert if >5% error rate |
| Email delivery failure | Log with booking ID | Daily summary to Ops Manager |
| Authentication failure | Log with IP (privacy safe) | Alert if spike detected |
| Validation error | Log with input data | No alert (user error) |

---

## Testing Requirements

### TR-1: Test Coverage Targets
**Priority**: P1 (Should Have)

| Test Type | Target Coverage | Tools |
|-----------|----------------|-------|
| Unit Tests | 70% code coverage | Jest, Vitest |
| Integration Tests | 60% critical paths | React Testing Library + Firebase Emulator |
| E2E Tests | 30% happy paths | Cypress |
| Manual Testing | 100% user journeys | Test cases documented |

---

### TR-2: Critical Test Scenarios
**Priority**: P0 (Must Pass Before Launch)

| Scenario | Expected Result |
|----------|-----------------|
| Member books available shift (auto-approve) | Booking approved, confirmation email sent |
| Member books shift needing approval | Booking pending, Ops Manager notified |
| Ops Manager approves pending booking | Booking approved, member notified |
| Member cancels within 3 days | Warning shown, Ops Manager notified |
| Coverage gap within 3 days | Ops Manager receives alert email |
| Shift reminder 3 days before | Member receives reminder email |
| Shift reminder 24 hours before | Member receives reminder email |
| Member indicates Fire Crew interest | Interest saved, visible in Ops Manager reports |
| Ops Manager updates training status | Training status updated, reflected in profile |
| Blackout date created | No shifts bookable on that date |

---

## Deployment Requirements

### DEP-1: Production Deployment
**Priority**: P0 (MVP Critical)

| Requirement | Specification |
|-------------|---------------|
| Hosting | Firebase Hosting with custom domain |
| Domain | volunteers.herefordshireaeroclub.co.uk (or similar) |
| SSL Certificate | Automatic via Firebase (Let's Encrypt) |
| CDN | Firebase Hosting global CDN |
| Deployment Method | GitHub Actions CI/CD pipeline |
| Rollback Capability | Previous version retained, 1-click rollback |
| Environment Variables | Stored in GitHub Secrets |
| Database Backup | Daily automatic via Firebase |

---

### DEP-2: Monitoring & Alerts
**Priority**: P0 (MVP Critical)

| Monitor | Threshold | Alert Recipient |
|---------|-----------|-----------------|
| Hosting uptime | <99% in 24 hours | Product Manager + Ops Manager |
| Cloud Functions errors | >5% error rate in 5 mins | Product Manager |
| Email delivery failures | >10% in 1 hour | Ops Manager |
| Database read/write errors | Any spike | Product Manager |
| Page load time | >3 seconds (p95) | Product Manager |
| Firebase costs | >£10/day | Product Manager |

---

## Launch Requirements

### LR-1: Pre-Launch Checklist
**Priority**: P0 (Must Complete)

- [ ] All P0 functional requirements implemented and tested
- [ ] Security audit completed (Firestore Rules, Auth config)
- [ ] Performance testing passed (page load <2s)
- [ ] Accessibility audit passed (WCAG 2.1 AA)
- [ ] Browser compatibility tested (Chrome, Firefox, Safari, Edge, Mobile)
- [ ] Email templates tested (all 8 types)
- [ ] Privacy policy published and linked
- [ ] Terms of service published and linked
- [ ] Cookie consent banner implemented
- [ ] User documentation written (Quick Start Guide, FAQ)
- [ ] Ops Manager training completed
- [ ] Beta testing with 10 members completed
- [ ] Feedback incorporated from beta testing
- [ ] Monitoring and alerting configured
- [ ] Backup and recovery tested
- [ ] Rollback plan documented
- [ ] Launch communication prepared (email, posters)

---

### LR-2: Post-Launch Requirements
**Priority**: P0 (First 30 Days)

- [ ] Daily check-ins with Ops Manager (first week)
- [ ] Weekly usage reports (members registered, shifts booked)
- [ ] Bug triage and fixes (within 48 hours for critical, 1 week for minor)
- [ ] User feedback collection (survey at 2 weeks)
- [ ] Performance monitoring (daily dashboard review)
- [ ] Cost monitoring (weekly Firebase usage check)
- [ ] Phase 1 success metrics review (at 30 days)

---

## Dependencies

### External Dependencies

| Dependency | Version | Purpose | Fallback |
|------------|---------|---------|----------|
| Firebase | 10+ | Backend infrastructure | None - critical |
| SendGrid | Latest | Email delivery | Manual email notifications |
| React | 18+ | Frontend framework | None - critical |
| Tailwind CSS | 3+ | Styling | Custom CSS (major work) |
| Lucide React | 0.263+ | Icons | Alternative icon library |

---

### Internal Dependencies

| Phase 1 Depends On | Provided By |
|--------------------|-------------|
| User accounts and training data | Ops Manager manual entry (first 2 weeks) |
| Shift requirements (dates, types) | Ops Manager creates in system |
| Member registration | Members self-register after launch |
| Beta testing feedback | 10 volunteer members |
| Domain and email configuration | Club IT administrator |

---

*Document Version: 1.0*  
*Last Updated: October 1, 2025*  
*Part of: Herefordshire Aeroclub Member Platform Specification*