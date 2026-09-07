---
title: Red Item Remediation Update
status: active
updated: 2026-09-07
owner: Alistair
related: ["[[00 Commercial Readiness Dashboard]]", "[[Data Retention Schedule]]", "[[Data Subject Rights Procedure]]", "[[Subprocessor Register]]", "[[DPIA]]", "[[Data Breach and Incident Response]]", "[[Stage 20 Backup Implementation]]", "[[Stage 21 Restore Test]]", "[[00 Solicitor Review Pack 2026-09-07]]"]
---

# Red Item Remediation Update - 7 September 2026

This note records the current evidence-led position after checking the AlistraGIS `main` repository and the Alistra Knowledge Vault. It deliberately distinguishes controls that are implemented, controls that are documented but not yet technically enforced, and matters that require professional legal/privacy judgement.

## Executive result

### Green / evidenced

- Firestore Point-in-Time Recovery is enabled and daily Firestore backups are active with 30-day retention.
- A separate append-only Storage mirror is documented and verified.
- An isolated Firestore restore test passed on 2026-08-11 without modifying production.
- Current recovery evidence records a managed database restore time of 627.893 seconds (10 minutes 27.893 seconds).
- The repository contains a Cloud Storage lifecycle configuration that deletes non-current object versions after 30 days.
- Storage profiles contain explicit backup-policy and data-policy fields, including `retentionDays`, `deletionAfterTerminationDays` and `exportRequiredOnTermination`.
- Whole-company backup-and-delete exists in the current `main` branch and recursively deletes the business Firestore tree, company Storage content and company Auth users (subject to the documented caller/owner safeguards).
- Support-ticket creation/status/assignment flows are business-scoped and role-gated.
- The previously empty Data Breach and Incident Response note has now been populated with an operational incident-response runbook.

### Amber / prepared but not fully implemented

- Data Subject Rights procedure exists and the current product has partial deletion/export capabilities, but there is no single DSAR-specific per-user locator/export/erasure workflow across all data stores and historical references.
- DPIA is substantially drafted and has been corrected to recognise that backup/restore testing is complete; professional privacy/legal review remains required.
- Subprocessor inventory is drafted from actual code/providers, but live DPA/region/log-retention/transfer settings still need account-level confirmation.
- Disaster recovery is materially implemented, but wider frontend rollback, selective Storage restore, application cutover and deputy ownership exercises remain outstanding.

### Red / cannot honestly be marked complete yet

1. **Retention enforcement across application data.** The application stores retention-policy fields but no general scheduled retention worker has been evidenced that enforces them for tickets, audit events, asset change logs, evidence files or deletion backups.
2. **Unified DSAR tooling/runbook.** The product lacks one controlled admin workflow that locates, exports, deletes or minimises a single person's data across Auth, user profiles, tickets/events, employee links, audit/change history, files/photos and backups.
3. **Final legal retention periods.** Engineering can enforce periods once approved, but the actual legal/default periods should not be invented in code before solicitor/accountant/privacy review.
4. **Final controller/processor, transfer and liability decisions.** These remain legal decisions, not engineering decisions.

## Repository evidence reviewed

### `functions/src/index.ts`

The current `main` branch contains `backupAndDeleteCompany`, protected by platform-owner/SuperAdmin checks and explicit `DELETE <businessId>` confirmation. The function collects Firestore/Auth/Storage backup material, writes a manifest for activated companies, removes root user records for the company, recursively deletes the business Firestore document tree, deletes company Storage files and deletes company Auth users other than the caller. This is strong evidence for customer exit/whole-company deletion capability, but it is not a substitute for a per-data-subject erasure workflow.

The current ticket functions create business-scoped tickets and ticket events, allow administrators to view all tickets and update status/assignment, and record user identifiers/names. No retention/expiry behaviour is evidenced in those ticket flows.

### `functions/src/storage/storageProfile.ts`

The current storage profile model explicitly contains:

- `backupPolicy.retentionDays`;
- `dataPolicy.retentionDays`;
- `dataPolicy.deletionAfterTerminationDays`;
- `dataPolicy.exportRequiredOnTermination`.

The default Firebase profile enables daily backups and defaults backup retention to 30 days. These fields provide the configuration surface needed for a future retention worker, but the model itself does not enforce expiry.

### `docs/CLOUD_STORAGE_BACKUP_LIFECYCLE.json`

The repository contains a lifecycle rule that deletes non-current object versions 30 days after they become non-current. This improves backup/version hygiene, but it does not delete live application records or provide a complete data-retention solution.

## Work that can be completed without a solicitor

The following engineering/operations tasks can be designed and implemented without waiting for legal advice, provided configurable/default periods are not represented as final legal commitments:

1. Build a retention worker that reads approved policy values and supports dry-run/report-only mode before deletion.
2. Build a privacy/DSAR admin locator that can find a user across Auth, root/business user profiles, tickets/events, employee records, operational references, audit events and asset change logs.
3. Build scoped export output for a single data subject and record the export as a sensitive admin action.
4. Build a controlled minimisation/erasure runbook that can remove profile/auth data while preserving or anonymising records that must be retained for security/audit reasons.
5. Add an incident register and run a tabletop breach exercise.
6. Verify Google/Firebase, Vercel and other provider region/log/DPA settings in the live accounts.
7. Verify retention/lifecycle settings for the append-only Storage mirror and tenant-deletion backups.

## Work deliberately held for solicitor/privacy approval

- final default retention periods by data category;
- lawful-basis/retention exceptions for audit, security, accounting and dispute records;
- controller/processor/joint-controller allocation;
- international-transfer wording/mechanisms;
- final DPA wording;
- infrastructure liability caps/exclusions and operational-reliance language;
- final privacy-notice wording and publication approval.

## Current recommendation

Do not make risky production deletions merely to change a dashboard colour. The safest path is to finish the configurable engineering mechanisms, keep destructive actions in dry-run/manual approval mode until retention periods are approved, then have a UK technology/SaaS solicitor review the prepared legal pack and confirm the final policy values and contractual wording.
