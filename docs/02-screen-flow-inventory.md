# SchoolBridge — Screen & Flow Inventory

**Status:** Working document — next product deliverable.

The purpose of this inventory is to translate approved business requirements into explicit screens, user actions, rules, outcomes, and notifications before any production coding begins.

## Parent Mobile App

| ID | Screen | Purpose | Priority | Status |
|---|---|---|---|---|
| P01 | Login / OTP | Authenticate registered users and route by role | Must | **Defined v0.1** |
| P02 | Home Dashboard | Daily overview of each child | Must | To detail |
| P03 | Child Switcher | Switch between linked children | Must | To detail |
| P04 | Attendance | View daily / monthly / term attendance | Must | To detail |
| P05 | Homework | View subject-wise assignments and attachments | Must | To detail |
| P06 | Notices | View school / class announcements | Must | To detail |
| P07 | Fees | View dues, history, and payment state | Must | To detail |
| P08 | Payment | Initiate supported fee payment | Must/Phase 1B | To detail |
| P09 | Leave Request | Submit leave request | Must | To detail |
| P10 | Leave History | Track approved / rejected / pending requests | Must | To detail |
| P11 | Notifications | Consolidated alert timeline | Must | To detail |
| P12 | Calendar | View important school dates | Should | To detail |
| P13 | More / Settings | Profile, receipts, downloads, support | Should | To detail |


## P01 — Login / OTP Functional Specification

**Status:** Defined v0.1

### Personas
The login flow supports three Phase 1 personas:
- **Parent** — receives school updates and tracks linked child/children.
- **Teacher** — manages class-level work such as notices, parent communication, and meetings.
- **School Admin / Principal** — manages school-wide communication and user/record administration. Principal shares the School Admin persona in Phase 1.

### Login Identifier
- Mobile number only.
- No password, username, or email login in Phase 1.
- User enters a 10-digit Indian mobile number and receives an SMS OTP.

### Eligibility / Unregistered Number
- Access is allowed only when the mobile number exists in the school-authorized user records.
- Unregistered numbers are rejected.
- User message: **"This number is not registered with the school. Please check your number or contact the school office to get added."**
- Provide the school's contact number / **Call School Office** action where supported.

### OTP Rules
- OTP validity: **3 minutes / 180 seconds**.
- Resend becomes available after **45 seconds**.
- Maximum incorrect attempts per OTP: **3**.
- Wrong OTP message shows remaining attempts, e.g. **"Incorrect code. 2 attempts left."**
- Expired OTP message: **"Code expired. Tap Resend Code."**
- After 3 failed attempts, new OTP requests for that number are blocked for **15 minutes**.
- Lockout message: **"Too many failed tries. Try again in 15 minutes."**

### Post-Login Role Routing
After OTP verification, the system resolves the user's authorized role.

- **Parent — one linked child:** route directly to Child Dashboard / Feed.
- **Parent — two or more linked children:** show child selector, then route to selected child's dashboard.
- **Teacher:** route to Class Dashboard.
- **School Admin / Principal:** route to School Broadcast & Management Hub.

### Session Behaviour
Product intent: user should remain signed in on a trusted device and should not be asked for OTP on every app launch.

Implementation guardrail:
- Do **not** use a literally permanent authentication token.
- Use a short-lived access token plus a securely stored renewable session / refresh token.
- Session must support server-side revocation, logout, account disablement, and security-triggered re-authentication.
- Exact session lifetime will be finalized during security architecture.

### First Login Terms / Privacy
On first successful login, show a lightweight consent / acknowledgement sheet:

**Welcome to SchoolBridge**

"By continuing, you agree to our Terms of Service and Privacy Policy regarding student communications and school records."

Action: **I Agree & Continue**

Do not store only a boolean. Store at minimum:
- acceptance status
- Terms version
- Privacy Policy version
- acceptance timestamp
- user ID
- school / tenant ID

The acknowledgement is shown again only when a materially updated policy version requires renewed acceptance.

### Inputs
- Mobile number
- OTP

### Outputs
- Authenticated user session
- Resolved role
- Authorized school / tenant context
- Parent-child relationship context where applicable
- First landing screen based on role

### Permissions
- Authentication does not itself grant access to arbitrary school or student records.
- Subsequent authorization must enforce the user's school, role, and permitted child/class relationships.

### Audit Events
Record:
- OTP requested
- OTP verified successfully
- OTP verification failed
- lockout triggered
- successful login
- logout
- session revoked
- Terms / Privacy acceptance

Do not log the OTP value itself.

### Acceptance Criteria
1. Registered Parent, Teacher, and Admin mobile numbers can request an OTP.
2. An unregistered number cannot proceed to OTP-authenticated application access.
3. OTP expires after 180 seconds.
4. Resend is unavailable for the first 45 seconds.
5. Three incorrect attempts trigger a 15-minute lockout.
6. Successful login resolves the correct role and landing experience.
7. A parent with multiple linked children is prompted to select a child.
8. First login requires Terms / Privacy acknowledgement before entering the workspace.
9. Returning users remain signed in through a secure renewable session until logout, revocation, expiry/security policy, or account disablement requires re-authentication.
10. Authentication events are auditable without storing plaintext OTP values.


## Teacher Web Experience

| ID | Screen | Purpose | Priority | Status |
|---|---|---|---|---|
| T01 | Teacher Home | Daily work summary | Must | To detail |
| T02 | My Classes | Select assigned class / section | Must | To detail |
| T03 | Mark Attendance | Record daily attendance quickly | Must | To detail |
| T04 | Homework | Create / edit homework | Must | To detail |
| T05 | Class Notices | Publish targeted class communication | Must | To detail |
| T06 | Leave Review | Approve / reject assigned leave requests | Must | To detail |
| T07 | Student List | View students in assigned classes | Must | To detail |

## School Admin Web Portal

| ID | Screen | Purpose | Priority | Status |
|---|---|---|---|---|
| A01 | Admin Dashboard | School operational overview | Must | To detail |
| A02 | Student Management | Add / edit / import students | Must | To detail |
| A03 | Parent Management | Manage parent accounts / relationships | Must | To detail |
| A04 | Teacher Management | Manage teachers and class assignments | Must | To detail |
| A05 | Classes / Sections | Configure academic structure | Must | To detail |
| A06 | Attendance Admin | View / correct / report attendance | Must | To detail |
| A07 | Homework Oversight | View posted homework | Should | To detail |
| A08 | Notices | Create targeted school communication | Must | To detail |
| A09 | Leave Administration | Review and report leave workflow | Must | To detail |
| A10 | Fee Setup | Configure fees / dues / discounts | Must | To detail |
| A11 | Fee Dashboard | View collections / pending dues | Must | To detail |
| A12 | Imports / Exports | Bulk onboarding and controlled exports | Must | To detail |
| A13 | Roles & Access | Configure authorized users and roles | Must | To detail |
| A14 | School Settings | School-level configuration | Must | To detail |

## Screen Definition Template

For every screen above, complete the following before implementation:

- User / role
- Purpose
- Entry point
- Data displayed
- Inputs
- Available actions
- Business rules
- Validation rules
- Result / output
- Notifications / events generated
- Permissions
- Error / empty states
- Audit requirements
- Dependencies
- Acceptance criteria

## First End-to-End Flow to Define

**Attendance Alert Flow**

Teacher selects class → marks attendance → submits → system validates → attendance saved → absent student's parent identified → parent notification generated → parent opens SchoolBridge → sees child's attendance status and attendance history.
