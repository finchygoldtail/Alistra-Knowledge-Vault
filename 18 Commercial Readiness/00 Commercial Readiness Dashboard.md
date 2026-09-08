---
status: draft
updated: 2026-09-08
related: ["[[Current State Validation 2026-08-08]]", "[[Cost and Abuse Protection]]", "[[04 Data Retention Schedule]]", "[[05 Subprocessor Register]]", "[[06 DPIA]]", "[[07 Data Subject Rights Procedure]]", "[[18 DPA Requirements]]", "[[17 Customer Data Processing Agreement]]", "[[19 API Licence Requirements]]", "[[Stage 20 Backup Implementation]]", "[[Stage 21 Restore Test]]", "[[09 Disaster Recovery Plan]]", "[[2026-09-07 Red Item Remediation Update]]", "[[12 Data Protection Complaints Procedure]]", "[[13 Client Framework Agreement]]", "[[Client Pricing Pack]]", "[[16 UK Compliance Action Register 2026-09-08]]"]
---

# Commercial Readiness Dashboard

Control area for the AlistraGIS v1.0 commercial go-live programme.

This folder does not replace the existing legal, security, infrastructure or architecture vault sections. It links to them and records go-live status from the programme.

## Stage Status

| Stage | File | Status | Result |
|---|---|---|---|
| 11 | [[Cost and Abuse Protection]] | Complete | App Check live but not enforced (staged: watch metrics, then enable per service); per-user rate limiting live on twelve callables; Firestore TTL on the counters active. |
| 14 | [[04 Data Retention Schedule]] | Amber - mechanism pending | Policy/configuration surface exists. Storage profiles expose retention/deletion fields and non-current Storage versions have a 30-day lifecycle rule, but general application-data retention enforcement is not implemented. |
| 15 | [[05 Subprocessor Register]] | Amber - verification pending | Providers identified from implementation; live DPA/region/log-retention/transfer checks remain. |
| 16 | [[06 DPIA]] | Amber - professional review | Privacy risks assessed and backup/restore evidence updated; legal/privacy review remains required. |
| 17 | [[Data Subject Rights Procedure]] | Amber - tooling pending | Procedure updated for current 2026 timing/search rules; partial deletion/export capability exists. Unified per-person tooling and mock SAR remain. |
| 18 | [[17 Customer Data Processing Agreement]] + [[DPA Requirements]] | Draft created / solicitor review | Article 28-style customer DPA draft now exists and is linked to the Framework/hosting schedules. Final legal wording, role allocation, subprocessor/transfer facts and retention still require review. |
| 19 | [[API Licence Requirements]] | Solicitor review | API licence requirements prepared; final commercial/legal terms require review. |
| 20 | [[Stage 20 Backup Implementation]] | Complete | Firestore PITR/daily backups and a verified daily append-only Storage mirror are live. |
| 21 | [[Stage 21 Restore Test]] | Passed | Isolated restore completed in 10m 27.893s; data/index/security checks passed and the temporary target was removed. |
| 22 | [[09 Disaster Recovery Plan]] | Implemented / drills pending | Recovery priorities and failure scenarios documented; wider frontend/Storage/cutover drills and deputy assignment remain before pilot. |
| 23 | [[Data Breach and Incident Response]] | Drafted / exercise pending | Operational runbook exists. Incident owner/deputy, live register, contact verification and tabletop exercise remain. |
| 24 | [[12 Data Protection Complaints Procedure]] | Procedure added / implementation pending | Statutory complaints process documented. Support/in-app intake category, owner/deputy and end-to-end test remain. |
| 25 | [[13 Client Framework Agreement]] + [[14 Client Order Form and Service Schedule]] + [[15 Hosting and Data Responsibility Schedule]] | Drafted / solicitor review | Modular contract system now covers modules, seats, projects, hosting, implementation, support and data responsibilities. Liability/dispute wording requires professional review. |
| 26 | [[Client Pricing Pack]] + [[Client Quote Template]] | Working commercial model | Draft prices now cover core platform, modules, seat bands, projects, hosting, support, onboarding and API/AI. Margin and cloud-cost validation remain before public release. |
| UK compliance register | [[16 UK Compliance Action Register 2026-09-08]] | Live working register | Separates required, incomplete and not-currently-required controls; ICO fee and company website disclosure remain external actions. |
| Commercial billing architecture | [[Commercial Allocation Billing Architecture]] | Awaiting live test | Money-out chain complete and deployed. One real allocation taken through to a paid invoice on live Firebase remains; money in is not started. |

## 8 September 2026 legal/commercial update

The Vault now includes a modular client contract stack and a working commercial price book. The Framework Agreement is designed to remain stable while each Order Form captures the customer's selected modules, user count, project capacity, hosting model, support level, implementation work and price.

The contract stack now also includes [[17 Customer Data Processing Agreement]], so the customer-controller / AlistraGIS-processor requirements have moved from a requirements-only document to an actual draft schedule for solicitor redline.

The new Hosting/Data Responsibility Schedule separates Supplier-managed shared hosting, Supplier-managed dedicated hosting and customer-selected/customer-hosted models. It explicitly records that Firebase/GCP is the current production-supported hosting path and that Azure/AWS/PostGIS customer-hosted deployment remains subject to customer-specific provisioning and technical validation.

A statutory Data Protection Complaints Procedure has also been added. The operational product work still required is a dedicated privacy-complaint intake/register, assigned owner/deputy and mock complaint test.

The Data Subject Rights Procedure has been updated so SAR timing is no longer left as an unknown legal placeholder: the operational baseline is one month, with the permitted extension/clarification rules and reasonable/proportionate search standard reflected.

## 7 September 2026 evidence update

See [[2026-09-07 Red Item Remediation Update]] for the repository-backed review.

The current `main` repository confirms that `backupAndDeleteCompany` can create an exit backup for an activated company and then recursively delete its business Firestore tree, company Storage content and company Auth users subject to SuperAdmin/owner safeguards. This is strong whole-company exit/deletion capability, but it does not replace a per-data-subject DSAR workflow.

The storage-profile model contains `backupPolicy.retentionDays`, `dataPolicy.retentionDays`, `dataPolicy.deletionAfterTerminationDays` and `exportRequiredOnTermination`. A repository lifecycle rule also deletes non-current Storage object versions after 30 days. These are useful controls, but no general retention worker has yet been evidenced for live tickets, audit events, asset change logs, evidence files or other operational records.

## Current Go-Live Position

The largest remaining legal/engineering issues are now:

1. solicitor redline/approval of the Framework, DPA, SaaS Licence and Standard Terms;
2. approved retention periods plus retention enforcement;
3. unified/tested per-person DSAR workflow;
4. live subprocessor region/log/DPA/transfer verification;
5. complaints intake/register implementation;
6. company registered-office/web disclosure resolution;
7. ICO fee self-assessment/registration where required;
8. incident-response tabletop and remaining DR drills;
9. pricing-margin and hosting-cost validation before public price publication.

For a controlled pilot, the current Supplier-managed hosting path and tightly scoped/test-data-first approach remain preferable until customer-hosted acceptance and final privacy/contract points are closed.

Final retention periods, controller/processor allocation, transfer mechanisms, liability caps and key negotiated terms remain matters for professional legal/privacy review. They must not be marked complete merely by changing documentation or inventing policy values in code.
