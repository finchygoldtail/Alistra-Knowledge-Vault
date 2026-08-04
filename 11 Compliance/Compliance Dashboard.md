# Compliance Dashboard

## Purpose
Central status page for AlistraGIS compliance, security and enterprise-readiness work.

## Current Status
| Area | Status | Owner | Next Action |
|---|---|---|---|
| GDPR programme | In progress | Product Owner | Complete data inventory and lawful-basis register |
| Firestore security | High priority | Engineering | Restrict audit-log writes and review tenant boundaries |
| Storage security | In progress | Engineering | Validate upload rules, file types and organisation isolation |
| Access control | In progress | Product + Engineering | Approve permission matrix and test every role |
| Audit logging | High priority | Engineering | Move trusted events to server-side logging and add retention controls |
| Support desk | Planned | Operations | Implement secure ticketing for access, password, incident and upgrade requests |
| Incident response | Draft | Security Lead | Assign named responders and test escalation paths |
| Disaster recovery | Draft | Engineering | Define RPO/RTO and run restore test |
| Privacy documentation | Draft | Product Owner | Obtain legal review before external publication |
| Enterprise readiness | In progress | Product Owner | Close critical controls and prepare evidence pack |

## Priority Actions
1. Prevent direct client creation, modification or deletion of trusted audit records.
2. Confirm strict organisation and project isolation in Firestore and Storage.
3. Add a controlled support-desk workflow for password resets, access changes, incidents and upgrades.
4. Complete the data map, retention schedule and deletion workflow.
5. Test backup restoration and incident-response procedures.

## Evidence Register
Store links to rule tests, penetration-test reports, DPIAs, supplier agreements, restore-test results, access reviews and policy approvals here.

## Review Cadence
- Critical security actions: weekly.
- Compliance roadmap: monthly.
- Policies and permission matrix: quarterly and after major releases.
- Full enterprise-readiness review: before each customer onboarding or material architecture change.
