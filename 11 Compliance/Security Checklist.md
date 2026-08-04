# Security Checklist

## Identity and Access
- [ ] MFA enforced for admin and super-admin accounts.
- [ ] Named accounts used; no shared privileged logins.
- [ ] Joiner, mover and leaver process tested.
- [ ] Privileged access reviewed monthly.
- [ ] Concurrent-session/licensed-seat controls documented and tested.

## Application and API
- [ ] Every privileged action is authorised server-side.
- [ ] Input schemas, rate limits and request IDs are implemented.
- [ ] Secrets are outside source control and rotated appropriately.
- [ ] Production and test environments are separated.
- [ ] Dependency and vulnerability scanning runs in CI.

## Firestore and Storage
- [ ] Unauthenticated access is denied.
- [ ] Cross-tenant negative tests pass.
- [ ] Trusted audit records cannot be forged, changed or deleted by clients.
- [ ] Immutable ownership/security fields are protected.
- [ ] File paths, size, type and metadata are validated.
- [ ] Temporary exports and signed links expire.

## Logging and Monitoring
- [ ] Duplicate asset-view logging has been removed or controlled.
- [ ] Privilege changes, exports and destructive actions are logged.
- [ ] Alerts exist for abuse, access failures and unusual activity.
- [ ] Log access and retention are reviewed.

## Privacy and Data Lifecycle
- [ ] Data inventory and ROPA are current.
- [ ] Lawful bases and DPIA triggers are documented.
- [ ] Retention and deletion jobs are tested.
- [ ] Data-subject request workflow is operational.
- [ ] Customer exit/export/deletion process is documented.

## Resilience and Response
- [ ] Backup jobs are monitored.
- [ ] Full restore test has succeeded.
- [ ] RPO/RTO are approved and evidence-based.
- [ ] Incident contacts and escalation paths are current.
- [ ] Incident tabletop exercise completed in the last 12 months.

## Enterprise Release Gate
- [ ] No open Critical security findings.
- [ ] High findings have owners and deadlines.
- [ ] Penetration testing completed for the production architecture.
- [ ] Support desk and security escalation are live.
- [ ] Policies, contracts and privacy wording have received appropriate review.
