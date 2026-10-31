# SchoolBridge — Independent Review of P01 and P02 (against `develop`)

| | |
|---|---|
| **Date** | 2026-10-31 |
| **Status** | PROPOSAL for founder review. Nothing here is approved. |
| **Reviewed** | `develop` @ `594d5af`: P01 and P02 "Defined v0.1", DEC-006, DEC-007, plus `README.md`, `CONTRIBUTING.md`, product definition |
| **Files modified** | None. This is a single new file under `docs/proposals/`. |
| **Approach** | MVP-first, in line with DEC-006. Every finding is tagged with **when** it is needed so nothing here delays the MVP unnecessarily. |

**Status key:** *Addressed* = already settled by the v0.1 spec. *Partial* = started but incomplete. *Open* = not covered.
**When key:** *Before build* = decide before engineering starts on that area. *Before launch* = needed for a pilot or store release. *Later* = post-MVP candidate.

Finding IDs (for example `P01-R4`) are stable so founders can approve or reject items in PR comments.

---

## 1. Top decisions to make first

1. **Attendance "Not marked yet" (P02).** The dashboard shows only Present, Absent or Late. A teacher who has not yet submitted attendance must not look like "Present" or blank. Add Not marked yet, Holiday, No school and On approved leave.
2. **One number, two roles (P01).** A teacher who is also a parent is common. Role routing does not say where they land. Propose a role chooser at login and a role switcher afterwards.
3. **Lockout can be used against a parent (P01).** OTP requests for a number are blocked for 15 minutes after 3 failed attempts, so a stranger could lock a real parent out. Lock by device and number pair, and add request throttling and bot protection (OTP endpoints are a known target for SMS-cost abuse).
4. **"This number is not registered" message (P01).** It tells anyone which numbers are registered. Decide: keep it for simplicity (with rate limits) or use a neutral message.
5. **Scope: "Contact / Message School" and teacher "parent communication, meetings".** The product definition has no messaging in the initial scope. DEC-006 favours a lean MVP. Decide whether two-way messaging is in or out.
6. **Payments phase.** P08 is "Must/Phase 1B" in the inventory, but P02 has a "Pay / View Fees" quick action. Decide Phase 1 or 1B and what the card does until payments exist.
7. **Homework "pending count" (P02).** A pending count implies parents or students mark homework done. The baseline has no completion tracking. Show a "due" count instead, or add tracking explicitly.
8. **Start SMS provider selection and DLT registration now,** and get legal advice on children's data and consent. Neither depends on design, and both can have long lead times.

---

## 2. What `develop` already settles

- Mobile number plus SMS OTP only, with the OTP rules (180 s validity, 45 s resend, 3 attempts, 15 min lockout) and clear error copy.
- Three personas (Parent, Teacher, School Admin/Principal) with role-based landing.
- Renewable session with server-side revocation, logout and disablement; no permanent tokens.
- First-login Terms/Privacy acceptance stored with versions, timestamp, user and tenant.
- A full audit event list, with no plaintext OTP logged.
- Dashboard: one child at a time, summary-plus-navigation, defined empty states, no data mixed between siblings, and a modular and extensible principle.

---

## 3. P01 — Login / OTP

| ID | Finding | Status | When | Suggestion |
|---|---|---|---|---|
| P01-R1 | Eligibility: only registered numbers | Addressed | | See P01-R1b |
| P01-R1b | Rejection message reveals that the number is unregistered | Open | Before launch | Decision #4 above |
| P01-R2 | One number may link to several children | Addressed | | |
| P01-R2b | Same number used by two parents, or one person in two schools | Open | Before build | Decide if a number can belong to more than one school (affects tenancy) |
| P01-R2c | **New:** same person is both Teacher and Parent | Open | Before build | Decision #2 above |
| P01-R3 | Number change or recycling | Open | Before launch | Admin-only change in A03 with audit; revoke old sessions; re-verify by OTP |
| P01-R4 | OTP policy values | Addressed | | |
| P01-R4b | **New:** per-number lockout can block a victim; no per-device or IP limits, and no cap on resends per hour | Open | Before build | Decision #3 above |
| P01-R4c | Country: spec is a 10-digit Indian number | Partial | Before launch | Confirm that parents abroad are excluded for the MVP |
| P01-R5 | Session approach (token plus renewable session) | Addressed | | |
| P01-R5b | Lifetime, inactivity expiry, device limit, revocation speed, re-auth before payment, optional app lock | Open | Before build (security architecture) | Proposed: 30-day inactivity expiry, max 3 devices, re-auth for payment |
| P01-R6 | Account states: invited, suspended, removed; all children withdrawn | Partial | Before launch | Define what each state sees |
| P01-R7 | First-login consent with versioning | Addressed | | |
| P01-R7b | Legal roles of school and SchoolBridge for children's data; parental consent under India's DPDP Act 2023 and rules; app-store account-deletion rules | Open | Before launch | Get legal advice; confirm current commencement dates |
| P01-R8 | Push permission timing and device-token registration | Open | Before build | Ask after login with context; register per device; remove on logout |
| P01-R9 | Language selection | Open | Before build | Decide v1 languages |
| P01-R10 | Reviewer or demo login for app-store review | Open | Before launch | Demo school with test data only |
| P01-R11 | Audit events | Addressed | | |
| P01-R11b | Retention period for audit logs | Open | Before launch | |
| P01-U1 | SMS delayed or failing: no fallback beyond resend | Open | Before launch | Add a visible countdown and "Call School Office" (already in spec); consider voice or WhatsApp OTP later |
| P01-U2 | Wrong number typed: no "Change number" | Open | Before build | Show the number on the OTP step with Change |
| P01-U3 | OTP autofill and paste | Open | Before build | Platform autofill; 6-box entry with paste |
| P01-U4 | Tapping a push notification while signed out | Open | Before launch | Return to the intended screen after login |
| P01-U5 | Accessibility and low-literacy support | Open | Before launch | Screen-reader labels, large targets, icons with text |
| P01-T1 | SMS gateway with India DLT registration (entity, header, template) | Open | **Start now** | Lead time can be days to weeks; plan a second provider |
| P01-T2 | Auth service: hashed OTP, rate limiting, token issuance, device registry, revocation | Open | Before build | |
| P01-T3 | Tenant, Parent, Student, Guardian-link data model; normalise phone numbers (E.164) at import (A12) | Open | Before build | |
| P01-T4 | Push infrastructure (FCM, APNs) | Open | Before build | |
| P01-T5 | Secure token storage; staging with test numbers; monitoring of OTP delivery | Open | Before build | Test OTPs in staging only |
| P01-I1 | Improvement: platform OTP autofill so most users never type the code | Open | Later | |
| P01-I2 | Improvement: show school name and logo after login to confirm context | Open | Later | Never before authentication |

---

## 4. P02 — Home Dashboard

| ID | Finding | Status | When | Suggestion |
|---|---|---|---|---|
| P02-R1 | One child at a time with a switcher | Addressed | | |
| P02-R1b | Two selectors: P01 post-login and P02 header | Partial | Before build | One shared component (see P03 proposal) |
| P02-R2 | Card list and order | Partial | Before build | Six cards plus quick actions will not fit one viewport; define the first-viewport set |
| P02-R3 | **Attendance states** | Open | Before build | Decision #1 above |
| P02-R4 | Freshness: no "updated at" or refresh behaviour; timezone IST | Open | Before build | Add timestamp and pull to refresh |
| P02-R5 | Homework "pending count" | Open | Before build | Decision #7 above |
| P02-R6 | Fees card: show rules, threshold, school-level visibility switch, payments off state, ₹ formatting | Partial | Before build | Proposed: show when due within 7 days or overdue; neutral wording |
| P02-R7 | "Most relevant" notice: rules undefined (urgent flag, expiry, targeting precedence) | Open | Before build | |
| P02-R8 | Leave status is listed under "Important Today" but has no card; approved leave should feed attendance | Open | Before build | |
| P02-R9 | Per-guardian permissions (for example restricted guardians) | Partial | Before launch | The spec says "data the school permits for the parent role"; define per-guardian flags in A03 |
| P02-R10 | Student status and academic-year rollover (transferred, withdrawn, mid-year admission) | Open | Before launch | |
| P02-R11 | Disabled modules and feature flags | Partial | Before build | Hide a disabled card instead of showing an empty one |
| P02-R12 | Empty states | Addressed | | |
| P02-R12b | Offline behaviour; one failing card must not blank the screen | Open | Before build | Cache with "last updated" banner; per-card errors |
| P02-R13 | "Recent Updates" feed overlaps P11 Notifications timeline | Open | Before build | Define the difference, and make unread counts come from one source |
| P02-R14 | Lock-screen push previews for child data | Open | Before launch | Make previews configurable |
| P02-U1 | Information overload above the fold | Open | Before build | See P02-R2 |
| P02-U2 | Colour-only status (red/green) | Open | Before build | Add icon and text |
| P02-U3 | Fee wording that causes anxiety | Open | Before launch | Neutral language; red only for overdue |
| P02-U4 | Wrong-child confusion | Partial | Before build | Child name, class and avatar on every card; selection persists |
| P02-U5 | Slow networks and low-end phones | Open | Before build | Skeleton loading, cache, small payloads |
| P02-U6 | Notification fatigue | Open | Later | Urgency model; optional digest |
| P02-T1 | Aggregated dashboard API returning per-card payloads and status (fits the modular guardrail) | Open | Before build | |
| P02-T2 | Upstream data: attendance, homework, notices, leave, fees, calendar and terms | Open | Before build | Agree API contracts first, so P02 is not blocked |
| P02-T3 | Notification service and events (e.g. `attendance.submitted`) with idempotency and retries | Open | Before build | Shared with P11 |
| P02-T4 | Server-side relationship-based authorisation | Open | Before build | |
| P02-T5 | Time and calendar service: IST, holidays, terms | Open | Before build | |
| P02-T6 | Per-school feature flags; force-update mechanism; PII-safe analytics | Open | Before launch | |
| P02-T7 | Import data quality (A12) determines dashboard accuracy | Open | Before build | |
| P02-I1 | Improvement: "Needs attention" ordering (urgent notice, then fee overdue, then homework due) | Open | Later | |
| P02-I2 | Improvement: child avatars or colours | Open | Later | |

---

## 5. Consistency notes across the documents

| ID | Note |
|---|---|
| C1 | Landing screens named in P01 ("Child Dashboard / Feed", "Class Dashboard", "School Broadcast & Management Hub") do not match inventory IDs (P02, T01, A01). Map them. |
| C2 | P01 now covers Teacher and Admin web users but sits under "Parent Mobile App". Consider a shared "Authentication" group. |
| C3 | P01's Teacher persona mentions notices, parent communication and meetings, but not attendance, homework or leave review, which are in the product definition. |
| C4 | In `docs/decision-log.md` on `develop`, a blank line before DEC-006 breaks the table so DEC-006 and DEC-007 do not render as table rows. (Not changed here.) |
| C5 | `README.md` status and "next deliverable" do not yet reflect P01 and P02 defined and P03 next. (Owner's call.) |
| C6 | The README lists a `wireframes/` folder and a frozen wireframe v0.1, but the repo contains no wireframe files. |
| C7 | The Attendance Alert Flow is still undefined. Edge cases to settle: corrections after submit, late and half-day, which guardians are notified, failed delivery, approved leave for the day, holidays. |

---

## 6. Proposed decision-log entries (NOT applied)

IDs start at DEC-008 because DEC-006 and DEC-007 are taken on `develop`.

| ID | Proposed decision | Status |
|---|---|---|
| DEC-008 | Attendance display has an explicit "Not marked yet" state and never defaults to Present | Proposed |
| DEC-009 | A person with more than one role chooses a role at login and can switch later | Proposed |
| DEC-010 | The child selector is one shared component used after login and in the dashboard header (see P03 proposal) | Proposed |
| DEC-011 | OTP lockout is applied per device and number pair, with request throttling and bot protection | Proposed |
| DEC-012 | Start SMS provider selection and DLT registration immediately | Proposed |
| DEC-013 | Data-protection roles and the parental-consent approach are confirmed with legal counsel before launch | Proposed |
| DEC-014 | Decide P08 payments: Phase 1 or Phase 1B | Proposed |
| DEC-015 | MVP homework display is by due date, with no completion tracking | Proposed |

---

## 7. Open questions

| # | Question |
|---|---|
| Q1 | Can one number belong to more than one school? |
| Q2 | Teacher who is also a parent: role chooser at login? |
| Q3 | Keep "not registered" wording, or use a neutral message? |
| Q4 | Is two-way parent-school messaging in the MVP? |
| Q5 | Is P08 payments in Phase 1 or Phase 1B? |
| Q6 | Homework: due count only, or completion tracking? |
| Q7 | Which languages are required in v1? |
| Q8 | Attendance cut-off time for "Not marked yet", and who is alerted? |
| Q9 | Fee card visibility threshold, and can schools hide dues? |
| Q10 | Per-guardian restrictions in v1? |
| Q11 | Who owns SMS provider and DLT registration? |
| Q12 | Who advises on children's data and consent? |
