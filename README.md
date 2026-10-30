# SchoolBridge

**Working concept:** A simple parent-engagement platform for Indian private schools.

SchoolBridge connects schools and parents through a parent mobile app and a lightweight school/teacher web portal. The initial product focus is deliberately narrow: attendance, homework, notices, leave requests, and fees.

## Current Project Status

- Business requirements: Baseline defined by founders through prior ground research and discussions.
- Product concept board / wireframe: **v0.1 FROZEN**.
- Current phase: **UX / Product Definition**.
- Next deliverable: **Complete Screen & Flow Inventory**.
- Coding status: **Not started intentionally** until the product flows are agreed.

## Product Surfaces

- **Parent:** iOS / Android mobile app
- **Teacher / School Admin:** Web portal
- **Backend / Database:** To be designed only after screen flows and rules are approved

## Initial Product Scope

1. Attendance
2. Homework
3. Notices / announcements
4. Leave requests and approvals
5. Fee visibility and payments
6. Parent notifications
7. Student / parent / class administration needed to support the above

## Repository Structure

```text
schoolbridge/
├── mobile-app/      # Future Flutter mobile application
├── admin-portal/    # Future school / teacher web portal
├── backend/         # Future application services / APIs
├── database/        # Future database schema, migrations, seed data
├── docs/            # Product requirements, decisions, flows, architecture
├── wireframes/      # Approved/frozen and working wireframes
└── README.md
```

## Collaboration Model

The repository is the shared source of truth for the founders and AI-assisted product/development work.

Recommended branches once coding begins:

- `main` — stable / approved baseline
- `develop` — integrated work in progress
- `feature/<name>` — isolated feature development

Important product decisions should be recorded in `docs/decision-log.md`.
