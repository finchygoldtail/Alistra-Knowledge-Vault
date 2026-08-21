---
status: draft
updated: 2026-08-21
related: ["[[CURRENT_STATE_VALIDATION]]", "[[Cost and Abuse Protection]]", "[[04 Data Retention Schedule]]", "[[05 Subprocessor Register]]", "[[06 DPIA]]", "[[07 Data Subject Rights Procedure]]", "[[18 DPA Requirements]]", "[[19 API Licence Requirements]]", "[[Stage 20 Backup Implementation]]", "[[Stage 21 Restore Test]]", "[[09 Disaster Recovery Plan]]"]
---

# Commercial Readiness Dashboard

Control area for the AlistraGIS v1.0 commercial go-live programme.

This folder does not replace the existing legal, security, infrastructure or architecture vault sections. It links to them and records go-live status from the programme.

## Stage Status

| Stage | File | Status | Result |
|---|---|---|---|
| 11 | [[Cost and Abuse Protection]] | Complete | App Check live but not enforced (staged: watch metrics, then enable per service); per-user rate limiting live on twelve callables; Firestore TTL on the counters active. |
| 14 | [[04 Data Retention Schedule]] | Drafted | Policy drafted; enforcement not implemented. |
| 15 | [[05 Subprocessor Register]] | Drafted | Providers identified; DPA/region checks remain. |
| 16 | [[06 DPIA]] | Drafted | Privacy risks assessed; legal/privacy review required. |
| 17 | [[07 Data Subject Rights Procedure]] | Drafted | Procedure drafted; tooling/runbook gaps remain. |
| 18 | [[18 DPA Requirements]] | Drafted | Solicitor-input requirements created. |
| 19 | [[19 API Licence Requirements]] | Drafted | API licence requirements created. |
| 20 | [[Stage 20 Backup Implementation]] | Complete | Firestore PITR/daily backups and a verified daily append-only Storage mirror are live. |
| 21 | [[Stage 21 Restore Test]] | Passed | Isolated restore completed in 10m 27.893s; data/index/security checks passed and the temporary target was removed. |
| 22 | [[09 Disaster Recovery Plan]] | Implemented | Recovery priorities and all required failure scenarios are documented; three failover/restore drills and deputy assignment remain before pilot. |
| Commercial billing architecture | [[Commercial Allocation Billing Architecture]] | Awaiting live test | Money-out chain complete and deployed: the export now states the certified value, and subcontractor invoices are recorded and matched with a one-invoice-per-valuation guard. One real allocation taken through to a paid invoice on live Firebase is all that remains. Money in is not started. |

## Current Go-Live Position

Stages 20 and 21 are passed and the Stage 22 disaster-recovery plan is implemented. Before pilot, the DR exercises must still prove frontend rollback, selective Storage restoration and application cutover to a restored database, and a deputy recovery owner must be assigned. Stage 23 incident response is next. Other recorded commercial-readiness dependencies remain in their stage files.

Stage 11 closed on 2026-08-21: App Check and per-user rate limiting are both deployed. One step remains and it is not code -- App Check enforcement is a Firebase console setting, held back until verified requests hold near 100% for several days, because switching it on early locks out every real user.

Billing moved a long way on 2026-08-21 and is closer to done than it looked, because most of it already existed under another name: an allocation is an area, and the chain through to a certified value signed off by a second person was already running. What is left of the money-out side is not code -- it is one real allocation taken through to a paid invoice on live Firebase.

The gap that now stands out most is **enforcement rather than policy**: the Data Retention Schedule (stage 14) still enforces nothing, since the only automated deletion anywhere in the project is the TTL on rate limit counters.
