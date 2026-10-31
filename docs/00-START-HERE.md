# SchoolBridge — START HERE

This is the fastest orientation page for founders, reviewers, and AI-assisted contributors.

## 1. What exists today

SchoolBridge is currently in **Product Definition / UX Specification**, not production development.

### Defined so far
- Product baseline and initial MVP scope
- Frozen Product Concept Wireframe v0.1
- P01 — Login / OTP functional specification
- P02 — Parent Home Dashboard functional specification
- Parent/Teacher/Admin screen inventory
- MVP-first / extensibility decisions
- Delivery roadmap
- Technical architecture principles
- Security baseline
- AI collaboration / branch rules

### Not built yet
- No production Flutter mobile app
- No production admin portal
- No backend/API implementation
- No database schema/migrations
- No live OTP/SMS integration
- No payment integration

The UI Review Pack is a **visual product design reference**, not evidence that the screens are already coded.

## 2. Visual reference

**SchoolBridge UI Review Pack v0.1**
https://drive.google.com/file/d/1KxuujdOPCZrpEfT4v1Qly4gnxH1jR5e0/view?usp=drivesdk

This contains the frozen wireframe and current UI concepts including Login / OTP and Parent Dashboard.

## 3. Main files — read in this order

### A. Product definition
`docs/01-product-definition.md`

Use this to understand:
- what SchoolBridge is
- who the users are
- initial MVP scope
- intentionally out-of-scope capabilities

### B. MAIN functional source of truth
`docs/02-screen-flow-inventory.md`

**This is the most important file for current functionality.**

It contains:
- all planned Parent screens P01–P13
- Teacher screens T01–T07
- Admin screens A01–A14
- detailed P01 Login / OTP specification
- detailed P02 Parent Dashboard specification
- acceptance criteria and business rules

For any new product function/page/card/field, first check this file.

### C. Decision log
`docs/decision-log.md`

Do not silently reverse an approved decision. Proposed changes should be discussed and recorded here after approval.

### D. Delivery roadmap
`docs/03-delivery-roadmap.md`

Shows the intended sequence from product definition through architecture, first vertical slice, MVP, and pilot.

### E. Technical guardrails
`docs/04-technical-principles.md`

Important principle: build modularly so new fields, pages, cards, and modules can be added later without major rework.

### F. Security baseline
`docs/05-security-baseline.md`

Minimum identity, authorization, tenancy, audit, privacy, and secure-development rules.

### G. ChatGPT / Claude collaboration
`docs/06-ai-collaboration.md`

Explains how multiple AI workstreams should contribute without overwriting each other.

## 4. Current product progress

### Parent app
- P01 Login / OTP — **Defined v0.1**
- P02 Home Dashboard — **Defined v0.1**
- P03 Child Switcher — Next
- P04 Attendance — Pending
- P05 Homework — Pending
- P06 Notices — Pending
- P07 Fees — Pending
- P08 Payment — Pending
- P09 Leave Request — Pending
- P10 Leave History — Pending
- P11 Notifications — Pending
- P12 Calendar — Pending
- P13 More / Settings — Pending

Teacher/Admin detailed flows follow after the Parent MVP baseline is sufficiently defined.

## 5. How to propose a new function

Do **not** create production code just because a feature sounds useful.

For a proposed capability:

1. Identify which user needs it: Parent / Teacher / Admin.
2. Check whether it already exists in `docs/02-screen-flow-inventory.md`.
3. If missing, document:
   - purpose
   - user/role
   - entry point
   - minimum data shown/entered
   - actions
   - business rules
   - error/empty state
   - permissions
   - acceptance criteria
4. Clearly label it **PROPOSED** until founder review.
5. Use a `feature/*` or `review/*` branch.
6. Raise a pull request rather than modifying `main` directly.

## 6. Recommended Claude task

> Read `docs/00-START-HERE.md`, `docs/01-product-definition.md`, `docs/02-screen-flow-inventory.md`, and `docs/decision-log.md`. Review the UI Review Pack. Do not rewrite approved P01/P02 requirements. Identify high-value missing MVP functions or UX gaps and document them as PROPOSED additions on a review branch. Do not implement production code yet unless explicitly assigned.

## 7. Branches

- `main` — approved/stable baseline
- `develop` — integrated work in progress
- `review/claude` — isolated Claude review work
- `backup/2026-10-31-pre-claude` — frozen backup from before Claude collaboration

## 8. Product principle

**MVP first, extensible by design.**

We do not need every possible field before building. We need the minimum useful functionality, implemented in a way that lets us add fields, screens, and modules later without rebuilding the product.
