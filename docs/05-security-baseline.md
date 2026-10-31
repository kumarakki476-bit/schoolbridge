# SchoolBridge — MVP Security Baseline

This is a minimum engineering baseline for future implementation.

## Identity
- OTP authentication for approved mobile numbers
- Rate limiting and lockout for abuse
- Short-lived access tokens
- Renewable/revocable sessions
- Logout and account-disable revocation

## Authorization
- Tenant isolation by school
- Role-based access
- Parent-child relationship checks
- Teacher-class assignment checks
- Admin access limited to authorized school scope

## Data
- Encrypt data in transit
- Encrypt sensitive data at rest where supported
- No raw payment-card storage
- No plaintext OTP storage
- No secrets in GitHub
- No real student data in development

## Audit
Capture security-relevant events, including:
- login success/failure
- lockout
- session revocation
- role changes
- attendance changes
- fee/payment status changes
- policy/consent acceptance

## Secure Development
- Dependency scanning
- Static checks / linting
- Pull-request review
- Separate development and production environments
- Security testing before production pilot

## Privacy
- Collect only data needed for the feature
- Retain evidence of Terms/Privacy versions accepted
- Build deletion/retention requirements into later detailed design
