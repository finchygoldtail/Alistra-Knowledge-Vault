---
status: draft
updated: 2026-09-07
stage: 23
related: ["[[Security Overview]]", "[[Audit Logging]]", "[[DPIA]]", "[[Subprocessor Register]]", "[[Data Subject Rights Procedure]]", "[[Stage 20 Backup Implementation]]", "[[Stage 21 Restore Test]]", "[[09 Disaster Recovery Plan]]"]
---

# Data Breach and Incident Response

Operational draft for AlistraGIS commercial readiness and solicitor/privacy review. This document is deliberately separated into technical facts, operational actions and legal decisions. It is not legal advice and does not make the final decision on regulatory or customer notification.

## Purpose

Provide a repeatable process for detecting, containing, investigating, recording and recovering from security incidents or personal-data breaches affecting AlistraGIS, its customers, users, infrastructure, subprocessors or source-code/deployment systems.

## Current platform context

AlistraGIS currently uses Firebase Authentication, Firestore, Firebase Storage, Cloud Functions/Google Cloud services and Vercel deployment. Customer data is business-scoped by `businessId`; security controls, audit logging and tenant-isolation work are documented elsewhere in the vault. Firestore Point-in-Time Recovery and daily backups are live, a daily append-only Storage mirror is active, and an isolated Firestore restore test passed on 2026-08-11. See [[Stage 20 Backup Implementation]] and [[Stage 21 Restore Test]].

## Incident categories

Treat the following as incidents requiring a recorded assessment:

- suspected cross-tenant access or tenant-isolation failure;
- compromised user, administrator, platform-owner or developer credentials;
- unauthorised Firebase, Vercel, GitHub or cloud-console access;
- accidental disclosure, deletion, corruption or alteration of customer or personal data;
- exposed secrets, API tokens, service credentials or environment variables;
- malware, malicious upload, abuse or denial-of-service behaviour;
- unauthorised bulk export or unusual download activity;
- source-code or deployment compromise;
- subprocessor incident affecting AlistraGIS data;
- loss of availability significant enough to affect customer operations;
- lost/stolen device where active credentials or exported customer data may be accessible;
- incorrect permissions causing users to see information outside their authorised role.

## Severity model

| Severity | Example | Initial action |
|---|---|---|
| SEV-1 Critical | Confirmed cross-tenant disclosure, privileged-account takeover, major destructive compromise or widespread customer impact | Immediate containment, preserve evidence, platform owner leads response, legal/privacy review started immediately |
| SEV-2 High | Confirmed unauthorised access within one tenant, exposed secret with credible misuse risk, significant data loss or prolonged service failure | Contain promptly, rotate/revoke access, investigate scope, notify relevant customer contact according to contract/legal advice |
| SEV-3 Medium | Suspicious activity with limited evidence, permission/configuration defect caught before confirmed disclosure, recoverable operational incident | Investigate and remediate, record evidence and decision |
| SEV-4 Low | Benign alert, blocked abuse attempt, low-risk configuration issue with no evidence of access | Record where useful, remediate through normal security backlog |

## Immediate response runbook

1. **Open an incident record.** Record UTC time detected, reporter, systems involved, business/customer potentially affected, symptoms and current severity.
2. **Preserve evidence.** Save relevant audit-event IDs, deployment/commit identifiers, cloud/Vercel/GitHub logs, screenshots, timestamps and affected resource identifiers. Do not unnecessarily copy personal/customer data into ad-hoc locations.
3. **Contain.** Depending on the event, disable an account, revoke sessions, rotate a secret, disable a callable/feature, suspend a customer integration, roll back a deployment or restrict access.
4. **Protect production.** Avoid destructive investigation steps. Where recovery is required, use the approved backup/restore and disaster-recovery process.
5. **Determine scope.** Identify affected tenants, users, data categories, time window, access type (read/write/delete/export), persistence and whether the incident is ongoing.
6. **Assess data impact.** Determine whether personal data or commercially sensitive infrastructure data was accessed, changed, deleted, exported or made unavailable.
7. **Escalate legal/privacy questions.** The platform owner records the facts; the solicitor/DPO/privacy adviser confirms any regulatory notification duties, timing, content and customer-contract obligations.
8. **Notify customers where required.** Use verified authorised contacts. State known facts, containment steps, customer actions and next update; do not speculate.
9. **Recover and verify.** Restore service/data using tested recovery controls; verify tenant isolation, permissions and data integrity before declaring recovery complete.
10. **Close with review.** Record root cause, impact, evidence, actions, unresolved risks, preventive work, owners and completion dates.

## Incident record minimum fields

- incident ID;
- detected date/time (UTC);
- incident owner;
- current severity and changes to severity;
- affected service/provider;
- affected customer/business IDs;
- affected user IDs or data categories where known;
- first known event and last known event;
- access type: read/write/delete/export/availability;
- containment actions and timestamps;
- credentials/secrets rotated;
- backups/restores used;
- evidence locations;
- customer communications;
- legal/privacy assessment and adviser;
- regulator notification decision, if applicable;
- root cause;
- corrective/preventive actions;
- closure approval.

## Customer and regulator notification decision

Do not make a notification decision solely from an engineering severity label. Prepare a factual incident summary for the solicitor/DPO/privacy adviser covering:

- what happened and when;
- categories and approximate volume of data affected;
- whether data was merely exposed, actually accessed, altered, deleted or exported;
- categories of people affected;
- infrastructure/customer confidentiality implications;
- likely consequences;
- containment and mitigation already completed;
- whether the customer is acting as controller and AlistraGIS as processor for the affected data;
- contractual notification clauses that apply.

The final customer/regulator notification wording and statutory deadlines must be confirmed against the final DPA, customer contract and applicable data-protection law.

## Subprocessor incidents

If Google/Firebase/GCP, Vercel, NVIDIA or another approved provider reports an incident:

1. preserve the provider notice and incident reference;
2. determine which AlistraGIS services/data were actually involved;
3. map affected customers/tenants;
4. follow the same legal/privacy assessment as an internally detected incident;
5. track provider remediation and evidence until closure;
6. update [[Subprocessor Register]] if the event changes the risk assessment or contractual controls.

## Recovery evidence already available

- Live Firestore PITR and scheduled backups: [[Stage 20 Backup Implementation]].
- Verified daily append-only Storage mirror: [[Stage 20 Backup Implementation]].
- Isolated Firestore restore passed with production left unchanged: [[Stage 21 Restore Test]].
- Wider service failover/cutover exercises remain tracked in [[09 Disaster Recovery Plan]].

## Outstanding work before commercial pilot

| ID | Requirement | Priority | Status |
|---|---|---|---|
| IR-01 | Nominate primary incident owner and deputy | P1 | Required |
| IR-02 | Create the live incident register/location and restrict access appropriately | P1 | Required |
| IR-03 | Confirm customer-security/privacy contact route and emergency contact details in onboarding/order form | P1 | Required |
| IR-04 | Solicitor/DPO review of notification decision process, contract wording and applicable deadlines | P1 | Required |
| IR-05 | Run one tabletop breach exercise including a mock cross-tenant disclosure scenario | P1 | Required |
| IR-06 | Run remaining DR failover/cutover drills recorded in [[09 Disaster Recovery Plan]] | P1 | Required |
| IR-07 | Confirm access to required Vercel/GCP/Firebase/GitHub security logs and their retention | P1 | Required |

## Current status

**Drafted for review, not yet operationally signed off.** The technical backup/restore capability is materially stronger than when the original empty Stage 23 note was created, but incident ownership, legal-notification review, evidence/log access verification and a tabletop exercise remain go-live actions.
