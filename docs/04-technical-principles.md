# SchoolBridge — Technical Principles

These principles guide future architecture and code. They are guardrails, not final technology decisions.

1. **Modular by default**
   - Features should be separable so new screens/modules can be added without rewriting unrelated code.

2. **Business logic outside UI**
   - Screens render state and collect actions; business rules belong in services/domain logic.

3. **API-first boundaries**
   - Mobile and web clients should use documented backend APIs rather than direct database coupling.

4. **Multi-tenant from day one**
   - Every school is isolated logically; authorization must enforce tenant boundaries.

5. **Least privilege**
   - Parent, Teacher and Admin access is explicitly constrained by role and relationship.

6. **Additive evolution**
   - Prefer changes that add optional fields/endpoints instead of breaking existing clients.

7. **No secrets in source control**
   - Credentials, tokens and production keys must stay in managed secret stores / environment configuration.

8. **Audit important actions**
   - Authentication, role changes, attendance changes, fee status changes and consent events must be traceable.

9. **Use synthetic/demo data during development**
   - Never use real student data for development or demos unless formally approved and protected.

10. **Build one vertical slice before broad feature expansion**
    - Prove the full stack works end-to-end before implementing many disconnected modules.
