# SchoolBridge — Delivery Roadmap

## Current Phase
**Phase 0 — Product Definition**

Goal: remove enough ambiguity to build the MVP without over-designing the future product.

### Exit criteria
- Parent MVP screens P01–P13 defined
- Teacher/Admin MVP flows defined at the minimum level required
- Core end-to-end flows agreed
- MVP scope explicitly separated from later features

## Phase 1 — Technical Design
- High-level architecture
- Data model / tenancy model
- API boundaries
- Authentication / authorization design
- Notification approach
- Payment integration approach
- Environment strategy
- Security / audit baseline

## Phase 2 — Engineering Foundation
- Flutter mobile project
- Admin web project
- Backend project
- Database migrations
- Local/dev environments
- CI checks
- Seed/demo data
- Logging and basic observability

## Phase 3 — First Vertical Slice
Build one end-to-end flow:
**Login → child context → attendance → parent notification → dashboard**

Goal: prove mobile, backend, database, authorization and notifications work together.

## Phase 4 — Parent MVP
Add:
- Homework
- Notices
- Fees
- Leave
- Notifications
- Calendar / More

## Phase 5 — Teacher/Admin MVP
Add the minimum workflows required to operate the Parent MVP.

## Phase 6 — Pilot Readiness
- Demo data
- QA / security testing
- Pilot-school onboarding workflow
- Support / feedback mechanism
- Privacy / terms
- Production environment

## Phase 7 — Pilot + Learn
Run with a limited school/user group, capture usage and feedback, then prioritize expansion.

## Guiding Principle
Do not delay MVP to anticipate every future field or module. Prefer modular, extensible implementation over exhaustive upfront design.
