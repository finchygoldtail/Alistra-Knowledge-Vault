---
status: draft
updated: 2026-08-11
related: ["[[CURRENT_STATE_VALIDATION]]", "[[04 Data Retention Schedule]]", "[[05 Subprocessor Register]]", "[[06 DPIA]]", "[[07 Data Subject Rights Procedure]]", "[[18 DPA Requirements]]", "[[19 API Licence Requirements]]", "[[Stage 20 Backup Implementation]]"]
---

# Commercial Readiness Dashboard

Control area for the AlistraGIS v1.0 commercial go-live programme.

This folder does not replace the existing legal, security, infrastructure or architecture vault sections. It links to them and records go-live status from the programme.

## Stage Status

| Stage | File | Status | Result |
|---|---|---|---|
| 14 | [[04 Data Retention Schedule]] | Drafted | Policy drafted; enforcement not implemented. |
| 15 | [[05 Subprocessor Register]] | Drafted | Providers identified; DPA/region checks remain. |
| 16 | [[06 DPIA]] | Drafted | Privacy risks assessed; legal/privacy review required. |
| 17 | [[07 Data Subject Rights Procedure]] | Drafted | Procedure drafted; tooling/runbook gaps remain. |
| 18 | [[18 DPA Requirements]] | Drafted | Solicitor-input requirements created. |
| 19 | [[19 API Licence Requirements]] | Drafted | API licence requirements created. |
| 20 | [[Stage 20 Backup Implementation]] | Complete | Firestore PITR/daily backups and a verified daily append-only Storage mirror are live. |
| 21 | [[Stage 21 Restore Test]] | Passed | Isolated restore completed in 10m 27.893s; data/index/security checks passed and the temporary target was removed. |
| Commercial billing architecture | [[Commercial Allocation Billing Architecture]] | In progress | Parent boundary is separated from allocations; lifecycle and final billing controls remain open. |

## Current Go-Live Position

The resilience backup and restore gates are now passed. The remaining commercial-readiness blockers are retention enforcement, provider DPA/region confirmation, DSAR tooling/runbook, legal/privacy review, and final billing/lifecycle controls. Storage cross-project/cross-region replication remains a recommended resilience improvement rather than a Stage 20 blocker.
