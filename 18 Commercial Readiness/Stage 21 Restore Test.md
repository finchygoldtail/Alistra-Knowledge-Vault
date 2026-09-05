---
status: passed
updated: 2026-08-11
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

Passed on 2026-08-11. Three scheduled backups were `READY`; the newest was restored into an isolated database, validated, and deleted after evidence was saved. Production was never overwritten or repointed.

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

Passed.

| Item | Evidence |
|---|---|
| Source backup | `67b9c533-1534-46cc-8f0a-7c5127dbd641`, `READY` |
| Snapshot | 2026-08-11 03:27:23.564022Z |
| Isolated target | `restore-test-20260811` in `europe-west2` |
| Started | 2026-08-11 17:19:53.885683Z |
| Completed | 2026-08-11 17:30:21.778388Z |
| Managed database restore duration | 627.893 seconds (10 minutes 27.893 seconds) |
| Recovery-point gap at test start | 49,950.322 seconds (13 hours 52 minutes 30.322 seconds) |
| Restore state | `SUCCESSFUL`, 100/100 |
| Composite indexes | 16/16 `READY`; zero normalized definition differences from production |
| Security checks | Target anonymous read returned HTTP 403; 23 Firestore and 10 Storage rules tests passed |
| Production integrity | Original UID and update time unchanged; PITR enabled; three backups still `READY` |
| Cleanup | Temporary database deleted at 2026-08-11 17:33:47.502787Z; source backup retained |

Restored collection checks found 2 businesses, 29 user records, 96 map assets, 1 work pack, 1 ticket, 5 ticket events, 1,515 audit events and 206 asset change logs. Current production contained 101 map assets, 1,560 audit events and 221 asset change logs immediately after the restore; the differences are consistent with activity after the 03:27Z snapshot.

The observed recovery point is inside the internal 24-hour target. The measured duration is the managed database restore time, not a contractual full-service RTO. Firestore backups do not contain Firebase Security Rules, so any retained restore target must have an approved non-production rules configuration applied before client testing.

Detailed evidence: `C:\Projects\fibre-gis\docs\PHASE_20_21_RECOVERY_EVIDENCE_2026-08-11.md`.

## Related Files Reviewed

- `fibre-gis/docs/BACKUP_RECOVERY_AND_MFA.md`
- `fibre-gis/.firebaserc`
- `fibre-gis/firebase.json`
- `fibre-gis/functions/src/index.ts` (`backupAndDeleteCompany`)
- `fibre-gis/functions/src/storage/storageProfile.ts`
- [[Backup and Recovery]]
- [[Stage 20 Backup Implementation]]
