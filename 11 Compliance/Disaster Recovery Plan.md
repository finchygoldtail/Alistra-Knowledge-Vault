# Disaster Recovery Plan

## Objective
Restore AlistraGIS safely after data corruption, accidental deletion, provider failure, cyberattack or deployment failure.

## Recovery Targets
Define approved targets per customer tier. Initial planning targets:
- Critical identity/API services: RTO 4 hours, RPO 1 hour where supported.
- Core operational data: RTO 8 hours, RPO 4 hours.
- Non-critical analytics and derived data: RTO 24–48 hours.
These are targets only until tested and contractually approved.

## Dependencies
Firebase Auth, Firestore, Storage, Cloud Functions, Vercel, GitHub, DNS, maps, email/support services and any customer-selected AWS/Azure storage.

## Required Controls
- Automated backups or exports with documented frequency and retention.
- Separate backup credentials and restricted restore permissions.
- Version-controlled infrastructure, rules and application code.
- Tested rollback for application and database-rule releases.
- Offline record of critical contacts, domains, suppliers and recovery steps.
- Customer-specific recovery instructions for customer-hosted deployments.

## Recovery Process
Declare incident; freeze risky changes; identify last known good state; protect evidence; restore into an isolated environment; validate tenant isolation, record counts, attachments and permissions; approve production restoration; monitor; communicate; document gaps.

## Testing
Perform quarterly backup checks and at least annual full restore exercises. Record actual RPO/RTO, failed steps, missing dependencies and corrective actions.

## Limitations
A backup is not proven until successfully restored. Provider availability features do not replace customer-specific exports, tested procedures or ransomware-resistant recovery planning.
