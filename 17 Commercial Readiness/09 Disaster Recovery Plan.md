---
status: implemented
updated: 2026-08-11
stage: 22
source: "[[Backup and Recovery]]"
---

# Stage 22 Disaster Recovery Plan

Stage 22 control file for recovering AlistraGIS from destructive changes, failed deployments, provider outages and service degradation.

Authoritative technical runbook: `C:\Projects\fibre-gis\docs\DISASTER_RECOVERY_RUNBOOK.md`

Related evidence: [[Stage 20 Backup Implementation]], [[Stage 21 Restore Test]], [[Vercel Deployment]], [[Firebase Infrastructure]], [[Deployment Architecture]].

## Scope Checked

- GitHub `finchygoldtail/AlistraGIS` is the source of truth; `main` drives the Vercel frontend release.
- Vercel is the only current frontend host for `alistragis.com`, `www.alistragis.uk` and `alistragis.co.uk`.
- Firebase Hosting is redirect-only and is not a tested Vercel failover.
- Firebase project `fibre-gis-v2` supplies Authentication, Firestore, Storage and Cloud Functions.
- Firestore has PITR enabled in `europe-west2` and three ready scheduled backups.
- All 130 listed Cloud Functions were `ACTIVE` in `europe-west2` when checked on 2026-08-11.
- The production upload bucket and daily append-only upload mirror are enabled and verified.
- CARTO/OpenStreetMap, Esri, Nominatim and Overpass are external map dependencies.
- The application has tenant-scoped offline map-save recovery, persistent failed-upload recovery and a cached application shell.
- The full application suite passed 284/284 tests, including four offline-recovery safeguards.

## Recovery Priorities

1. Contain unsafe writes, unauthorised access and further data loss.
2. Preserve evidence and device-held pending field work.
3. Restore Authentication, trusted Firestore reads and the core frontend.
4. Restore safe writes, Functions and uploaded evidence.
5. Restore map helpers and other non-core providers.
6. Restore FRIDAY/AI last; AI failure must not affect core GIS.

## Scenario Coverage

| Required scenario | Runbook decision |
|---|---|
| Accidental deletion | PITR or scheduled backup restored into isolation first; Storage versions/soft delete/mirror used for files |
| Broken deployment | Roll back Vercel to a known-good Git deployment; redeploy only affected Firebase Functions/rules from tested source |
| Database corruption | Stop the corrupting writer, preserve evidence, restore clean data in isolation, validate before selective repair/cutover |
| Compromised credentials | Disable/revoke, preserve logs, rotate rather than merely delete, scope affected activity, re-enable only after verification |
| Firebase failure | Preserve local queues, use bounded offline/read-only operation, do not improvise an unimplemented backend failover |
| Vercel failure | Roll back if Vercel control plane works; otherwise communicate outage because no independent frontend host is currently tested |
| Map-provider failure | Switch CARTO/Esri basemaps where possible; use coordinate fallback for Nominatim; pause new Overpass imports |
| AI-provider failure | Fail closed and keep FRIDAY offline; core application continues |
| Service degradation | Narrow writes, preserve queues, restore reads before writes where integrity is uncertain, validate several tenants/roles/devices |

## Ownership

- Primary disaster commander/recovery owner: Alistair.
- Customer communications owner: Alistair until delegated.
- Deputy recovery owner: unassigned; must be appointed and access-tested before a controlled pilot.
- Evidence recorder: nominated at declaration and must record UTC timeline, actions, resource IDs, validation and communications.

## Result

The Stage 22 disaster-recovery plan is implemented and covers every scenario required by the pinned commercial go-live programme. It uses the proven Phase 20/21 backup and restore controls and distinguishes containment, recovery, validation and communication.

This is an operational plan, not a claim that every failover path is already tested. The following exercises remain mandatory before a controlled pilot:

1. Time a rollback to a previous Vercel production deployment.
2. Test selective restoration of one non-sensitive Storage object from the mirror/previous generation.
3. Test an application connection or controlled cutover to a named restored Firestore database.
4. Assign and access-test a deputy recovery owner.
5. Decide whether an independent frontend fallback is required for a Vercel platform outage.

These actions also feed Stage 24 monitoring, Stage 25 environment separation and Stage 29 release/rollback management. Stage 23 is next and must define incident/breach assessment, evidence preservation and notification decisions.

