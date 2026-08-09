---
status: draft
updated: 2026-08-08
stage: 14
source: "[[Data Retention Schedule]]"
---

# Data Retention Schedule

Stage 14 control file.

Detailed schedule: [[Data Retention Schedule]]

## Evidence Checked

- `fibre-gis/functions/src/index.ts` for `deleteLoginUser`, `backupAndDeleteCompany`, tickets and audit logs.
- `fibre-gis/functions/src/storage/storageProfile.ts` and `storageProfileManagement.ts` for retention/backup policy fields.
- `fibre-gis/functions/src/friday/fridayCallables.ts` for FRIDAY prompt/log retention.
- `fibre-gis/docs/BACKUP_RECOVERY_AND_MFA.md` for backup retention runbook.
- [[03 GDPR Data Register]] for the data categories.

## Result

Policy drafted, but not passed. Retention values exist in storage profile configuration, and manual deletion exists for selected entities, but no automated retention worker or approved legal retention periods are in place.

Priority: P1 before controlled pilot.
