---
status: complete
updated: 2026-08-11
stage: 20
source: "[[Backup and Recovery]]"
---

# Stage 20 Backup Implementation

Stage 20 control file.

Detailed infrastructure note: [[Backup and Recovery]]

Source runbook: `C:\Projects\fibre-gis\docs\BACKUP_RECOVERY_AND_MFA.md`

## Evidence Checked

- `fibre-gis/.firebaserc` confirms live project id `fibre-gis-v2`.
- `fibre-gis/firebase.json` confirms Firestore rules/indexes, Storage rules and Functions configuration are in source control.
- `fibre-gis/docs/BACKUP_RECOVERY_AND_MFA.md` defines PITR, daily Firestore backups, Storage backup requirements and restore-test process.
- `fibre-gis/functions/src/index.ts:1025`-`1122` implements `backupAndDeleteCompany`.
- `fibre-gis/functions/src/storage/storageProfile.ts:20`-`38` and `80`-`101` define backup policy fields.
- Live production upload bucket `gs://fibre-gis-v2.firebasestorage.app` has versioning and 30-day soft delete enabled.
- Private backup bucket `gs://fibre-gis-v2-upload-backups` has versioning, 30-day soft delete, uniform bucket-level access and public access prevention.
- Storage Transfer job `transferJobs/12826903455118721046` is enabled on a daily (`86400s`) append-only schedule.
- First transfer operation `transferOperations/transferJobs-12826903455118721046-6487464546522735147` completed successfully on 2026-08-11: 8/8 objects and 19,155,778/19,155,778 bytes copied, with all 8 names, sizes and checksums matching.
- Firestore and Storage security regression suites passed 33/33 tests after the live backup controls were applied.

## Result

Complete. Live Firestore Point-in-Time Recovery is enabled, a daily backup schedule with 30-day retention is active, and uploaded photos/documents now have a separately verified daily append-only mirror. The tenant-delete backup also exists in code. Restore proof is recorded separately in [[Stage 21 Restore Test]].

## Live Verification Commands

Live Firestore evidence:

```bash
gcloud firestore databases describe --database='(default)' --project='fibre-gis-v2'
gcloud firestore backups schedules list --database='(default)' --project='fibre-gis-v2'
```

## Residual Improvements

- Both Storage buckets are currently in the same Google Cloud project and `US-EAST1` region. A cross-project or cross-region copy would improve protection against project-wide or regional failure.
- The mirror does not propagate source deletions and the transfer service account cannot delete or overwrite destination objects. This is the deliberate recovery-safe design, but an approved retention-enforcement process is still required under [[04 Data Retention Schedule]].
- Upload residency in `US-EAST1` remains a Stage 15 DPA/region review item; changing region was outside this backup phase.
