---
title: Firebase Infrastructure
type: infrastructure
status: draft
owner: Alistair
created: 2026-08-02
updated: 2026-08-11
tags: [firebase, infrastructure]
---

# Firebase Infrastructure

Firebase provides Authentication, Firestore and Storage.

## Services

- Authentication for [[Authentication]].
- Firestore for [[Data Storage Strategy]].
- Storage for [[Files API]].

## 2026-08-09 Functions release

The mobile production completion backend was deployed to Firebase project `fibre-gis-v2` in `europe-west2` after commit `7ac3b4d` was pushed. `logCompanyDailyProduction` was checked after the CLI deployment and confirmed `ACTIVE`. The deployment command initially exceeded the local CLI timeout while Google Cloud was still processing updates; the final function listing confirmed the updated source hash and active state.

## 2026-08-11 Disaster-recovery baseline

Authenticated live checks for [[09 Disaster Recovery Plan]] confirmed:

- Firestore location `europe-west2`, PITR enabled and three scheduled backups `READY`.
- 130 listed Cloud Functions, all `ACTIVE` in `europe-west2`.
- Production uploads and the separate daily append-only mirror remain present.

The product currently has no automatic alternate Firebase backend. Offline device recovery protects pending work during bounded disruption but is not a backend failover.
