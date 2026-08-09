---
title: Firebase Infrastructure
type: infrastructure
status: draft
owner: Alistair
created: 2026-08-02
updated: 2026-08-09
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
