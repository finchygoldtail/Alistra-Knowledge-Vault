---
status: draft
updated: 2026-09-07
related: ["[[Current State Validation 2026-08-08]]", "[[Cost and Abuse Protection]]", "[[04 Data Retention Schedule]]", "[[05 Subprocessor Register]]", "[[06 DPIA]]", "[[07 Data Subject Rights Procedure]]", "[[18 DPA Requirements]]", "[[19 API Licence Requirements]]", "[[Stage 20 Backup Implementation]]", "[[Stage 21 Restore Test]]", "[[09 Disaster Recovery Plan]]", "[[2026-09-07 Red Item Remediation Update]]"]
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
| 17 | [[07 Data Subject Rights Procedure]] | Amber - tooling pending | Procedure and partial deletion/export capabilities exist. A unified per-person locator/export/erasure workflow is still required. |
| 18 | [[18 DPA Requirements]] | Solicitor review | Engineering requirements prepared; final legal terms require solicitor input. |
| 19 | [[19 API Licence Requirements]] | Solicitor review | API licence requirements prepared; final commercial/legal terms require review. |
| 20 | [[Stage 20 Backup Implementation]] | Complete | Firestore PITR/daily backups and a verified daily append-only Storage mirror are live. |
| 21 | [[Stage 21 Restore Test]] | Passed | Isolated restore completed in 10m 27.893s; data/index/security checks passed and the temporary target was removed. |
| 22 | [[09 Disaster Recovery Plan]] | Implemented / drills pending | Recovery priorities and failure scenarios documented; wider frontend/Storage/cutover drills and deputy assignment remain before pilot. |
| 23 | [[Data Breach and Incident Response]] | Drafted / exercise pending | Operational runbook now exists. Incident owner/deputy, live register, contact verification and tabletop exercise remain. |
| Commercial billing architecture | [[Commercial Allocation Billing Architecture]] | Awaiting live test | Money-out chain complete and deployed. One real allocation taken through to a paid invoice on live Firebase remains; money in is not started. |

## 7 September 2026 evidence update

See [[2026-09-07 Red Item Remediation Update]] for the repository-backed review.

The current `main` repository confirms that `backupAndDeleteCompany` can create an exit backup for an activated company and then recursively delete its business Firestore tree, company Storage content and company Auth users subject to SuperAdmin/owner safeguards. This is strong whole-company exit/deletion capability, but it does not replace a per-data-subject DSAR workflow.

The storage-profile model contains `backupPolicy.retentionDays`, `dataPolicy.retentionDays`, `dataPolicy.deletionAfterTerminationDays` and `exportRequiredOnTermination`. A repository lifecycle rule also deletes non-current Storage object versions after 30 days. These are useful controls, but no general retention worker has yet been evidenced for live tickets, audit events, asset change logs, evidence files or other operational records.

## Current Go-Live Position

The biggest engineering/privacy gap is now **enforcement and per-person tooling**, not backup/recovery. Stages 20 and 21 remain evidenced as complete/passed. Stage 22 is materially implemented and Stage 23 has an operational draft.

Before a controlled commercial pilot, priority technical work is:

1. configurable retention enforcement with dry-run/reporting before destructive deletion;
2. a unified DSAR locator/export/minimisation or erasure workflow;
3. live subprocessor region/log/DPA verification;
4. incident-response tabletop and remaining DR drills.

Final retention periods, controller/processor allocation, transfer mechanisms, DPA wording and liability terms remain matters for professional legal/privacy review. They must not be marked complete merely by changing documentation or inventing policy values in code.
