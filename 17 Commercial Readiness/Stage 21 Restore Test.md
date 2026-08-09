---
status: pending-first-backup
updated: 2026-08-08
stage: 21
source: "[[Backup and Recovery]]"
---

# Stage 21 Restore Test

Stage 21 control file for proving that the live backup configuration can restore usable project data without modifying production.

## Scope

- Source project: `fibre-gis-v2`
- Source database: `(default)`
- Source location: `europe-west2`
- Restore target: a separately named non-production Firestore database or approved isolated test project
- Production database must not be overwritten

## Preconditions

- [[Stage 20 Backup Implementation]] has Firestore PITR enabled and a daily scheduled backup with 30-day retention.
- A scheduled backup is visible before the test begins.
- An approved restore target name and owner are recorded.
- The operator has `roles/datastore.restoreAdmin` or equivalent restore permission.
- A test checklist and start/end timestamps are prepared.

## Current Position

The Firestore schedule was created on 2026-08-08 at 21:31 with 30-day retention. No scheduled backup was visible immediately afterward, so the restore test is pending the first available backup. PITR is enabled and reports a 7-day version retention period.

Check for an available backup:

```powershell
gcloud firestore backups list --location=europe-west2 --project=fibre-gis-v2
```

## Test Procedure

1. Record the selected backup name, creation time, source database, and target database name.
2. Confirm the target database does not contain production data that must be retained.
3. Restore the selected backup into the isolated target using the documented Firestore restore command.
4. Record the restore operation start and completion times, result, and any warnings.
5. Verify representative projects, users/roles, map assets, work packs, tickets, audit records, and relevant indexes in the target.
6. Confirm the production database remains unchanged.
7. Record the recovery duration, approximate recovery point, test operator, and evidence links.

## Acceptance Criteria

- Restore completes without modifying production.
- Target data is readable and structurally consistent with the selected backup.
- Representative tenant isolation and permission checks pass in the target.
- The measured restore duration and recovery point are recorded.
- Any missing data, configuration, or manual follow-up is documented.

## Result

Pending. The first scheduled backup must exist before the restore test can be executed.

## Related Files Reviewed

- `fibre-gis/docs/BACKUP_RECOVERY_AND_MFA.md`
- `fibre-gis/.firebaserc`
- `fibre-gis/firebase.json`
- `fibre-gis/functions/src/index.ts` (`backupAndDeleteCompany`)
- `fibre-gis/functions/src/storage/storageProfile.ts`
- [[Backup and Recovery]]
- [[Stage 20 Backup Implementation]]
