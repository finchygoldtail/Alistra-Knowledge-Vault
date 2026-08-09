---
title: Backup and Recovery
type: infrastructure
status: draft
owner: Alistair
created: 2026-08-02
updated: 2026-08-08
tags: [backup, recovery]
---

# Backup and Recovery

Stage 20 of the commercial go-live programme. This page records the backup implementation position for the live `fibre-gis` product and links to the detailed source runbook.

## Current Evidence

- Live Firebase project id in `C:\Projects\fibre-gis\.firebaserc`: `fibre-gis-v2`.
- Firebase config in `C:\Projects\fibre-gis\firebase.json` includes Firestore rules/indexes, Storage rules, Functions and redirect-only Firebase Hosting.
- Detailed source runbook exists at `C:\Projects\fibre-gis\docs\BACKUP_RECOVERY_AND_MFA.md`.
- `backupAndDeleteCompany` exists in Cloud Functions and creates a Storage manifest backup before deleting a company tree.
- Storage profiles include backup policy fields (`enabled`, `frequency`, `retentionDays`, `pointInTimeRecovery`) with a default backup retention of 30 days.

## Required Production Backup Controls

| Area | Required control | Current status |
|---|---|---|
| Firestore | Enable point-in-time recovery for `(default)` database | Enabled live on 2026-08-08; Firestore reports 7-day version retention |
| Firestore | Daily scheduled backups with defined retention | Enabled live on 2026-08-08; daily recurrence and 30-day retention |
| Firestore | Restore into a non-production database first | Runbook defined; test not yet evidenced in vault |
| Firebase Storage | Versioning or export/replication for uploaded files/photos/documents | Not verified |
| Source/config | Repository contains rules, indexes, functions, frontend source and deployment config | Present in `fibre-gis` |
| Secrets/config | Secret values kept out of repo and backed by provider controls | Covered by [[Secrets Audit 2026-08-08]]; console state not fully verified |
| Company deletion backups | Manifest backup before destructive tenant deletion | Implemented in `backupAndDeleteCompany`; backup expiry not implemented |
| Restore evidence | Timed restore test with result recorded | Not yet complete |

## Live Verification

On 2026-08-08, an authenticated read-only check was completed against project `fibre-gis-v2`:

```text
locationId: europe-west2
pointInTimeRecoveryEnablement: POINT_IN_TIME_RECOVERY_ENABLED
versionRetentionPeriod: 604800s
backupSchedule: projects/fibre-gis-v2/databases/(default)/backupSchedules/bea40eb8-54f0-40e0-8a66-267508b2e951
backupScheduleRetention: 2592000s
backupScheduleRecurrence: daily
```

Result: the live Firestore database has Point-in-Time Recovery enabled and a daily scheduled backup with 30-day retention. Firebase Storage backup/versioning still requires a separate live check, and restore evidence is not yet complete.

The earlier unauthenticated check from this machine was:

```powershell
firebase firestore:backups:schedules:list --database '(default)' --project fibre-gis-v2
```

Result: blocked because the Firebase CLI was not installed or on PATH at that time. It has since been superseded by the authenticated `gcloud` result above.

## Implementation Commands Used With Authenticated Tooling

These commands are already captured in the repo runbook and should be run by an authenticated operator with Firebase/GCP access:

```bash
gcloud firestore databases describe --database='(default)' --project='fibre-gis-v2'
gcloud firestore backups schedules list --database='(default)' --project='fibre-gis-v2'
```

The live scheduled backup was created with the agreed 30-day retention:

```bash
gcloud firestore backups schedules create \
  --database '(default)' \
  --retention 30d \
  --recurrence daily \
  --project fibre-gis-v2
```

Firestore backups do not include uploaded Firebase Storage files. Storage versioning, lifecycle/export policy and restore process must be configured and evidenced separately.

## Go-Live Position

Backup requirements are documented, and the codebase contains some backup-related controls, but Stage 20 is **not fully passed** until the live Firestore backup/PITR state and Storage backup policy are confirmed from the cloud console/CLI and recorded with evidence.

## Related

- [[Firebase Infrastructure]]
- [[Data Storage Strategy]]
- [[Client Hosted Deployment]]
- [[Data Retention Schedule]]
