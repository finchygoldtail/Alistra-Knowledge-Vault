# Enterprise Readiness

## Purpose
Define the minimum controls and evidence required before AlistraGIS is offered to enterprise customers or used for sensitive production workloads.

## Readiness Domains
| Domain | Minimum Evidence |
|---|---|
| Governance | Named owners, risk register, policy approvals and review dates |
| Privacy | Data map, ROPA, lawful bases, DPIA process, retention and rights workflow |
| Identity | MFA for privileged users, joiner/mover/leaver process and access reviews |
| Multi-tenancy | Proven tenant isolation across API, Firestore, Storage, exports and logs |
| Secure development | Peer review, dependency scanning, CI tests, release and rollback process |
| Logging | Server-side tamper-resistant audit events and actionable alerts |
| Resilience | Documented backups, tested restore, RPO/RTO and supplier dependencies |
| Incident response | Named responders, notification process and exercise evidence |
| Suppliers | Contracts, subprocessor list, security review and transfer safeguards |
| Customer operations | Support desk, SLAs, escalation, maintenance and change communication |

## Mandatory Launch Gates
- No unresolved Critical findings.
- High findings have approved remediation dates and compensating controls.
- Cross-tenant negative tests pass.
- Audit logs cannot be forged or deleted by ordinary clients.
- Backup restoration has succeeded in a representative environment.
- Privileged accounts use MFA and have been reviewed.
- Customer data location, ownership, exit and deletion terms are documented.
- Privacy and contractual documents have received appropriate professional review.

## Customer Evidence Pack
Architecture/data-flow diagrams, permission matrix, security overview, test reports, penetration-test summary, backup/restore evidence, incident plan, privacy documents, subprocessors, support model and current remediation register.

## Future Assurance
Consider Cyber Essentials/Plus, independent penetration testing, ISO 27001-aligned controls and SOC 2 readiness as customer and market requirements mature. Certification must never be claimed until formally achieved.
