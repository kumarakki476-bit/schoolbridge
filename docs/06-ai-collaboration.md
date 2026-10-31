# SchoolBridge — AI Collaboration Workflow

SchoolBridge may be worked on using ChatGPT, Claude and other development assistants. GitHub remains the single source of truth.

## Rules

1. **Do not push experimental work directly to `main`.**
2. Use `develop` for integrated work and `feature/*` or `review/*` branches for isolated changes.
3. AI-generated changes must be reviewable through commits / pull requests.
4. Do not allow an AI assistant to invent or silently change approved business requirements.
5. Proposed requirement changes must be clearly identified as proposals.
6. Never provide secrets, production credentials or real student data to an AI coding workflow.
7. Before merging significant code, record:
   - what changed
   - why
   - tests run
   - known limitations
8. Product decisions belong in `docs/decision-log.md`.

## Suggested Parallel Workflow

- **ChatGPT workstream:** product structure, functional specs, architecture, implementation/review
- **Claude workstream:** independent review, alternative design proposals, isolated coding experiments
- **GitHub:** shared record, branches, pull requests, issues, decisions

The goal is independent thinking with controlled reconciliation—not two assistants editing the same files blindly.
