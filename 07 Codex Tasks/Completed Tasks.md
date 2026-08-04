---
title: Completed Tasks
type: codex
status: active
owner: Alistair
created: 2026-08-02
updated: 2026-08-04
tags: [codex, completed]
---

# Completed Tasks

## Completed

- 2026-08-02: Created initial AlistraGIS Obsidian vault structure.
- 2026-08-04: Round-2 reliability/cost/security audit of `fibre-gis`, followed by a fix pass on the 2 Critical and 7 High findings (report: [Reliability, cost & security audit — Round 2](https://claude.ai/code/artifact/4eb9344d-8be3-4a04-9c47-9b31f275de3c)). Pushed to `main` on `finchygoldtail/AlistraGIS`. See [[Active Bugs]] for what's still open and [[Decision Log]] for the two decisions this raised.
	- Fixed: cable-draw mousemove handler scanned every map asset per raw pointer event with no throttling, causing visible lag while drawing on tablets. Now coalesced to one lookup per animation frame.
	- Fixed: field photo capture only attached uploaded photo URLs to an asset after the whole batch succeeded — a dropped connection mid-batch silently lost already-uploaded photos. Now persists per-photo as each upload completes, with retry for failures. See [[Field User Experience]], [[Offline Mode]].
	- Fixed: every asset save double-wrote the audit trail to two Firestore collections (`assetChangeLogs` + `assetActivityLogs`); the second had no reader anywhere in the app. Now writes once. See [[Audit Logging]].
	- Fixed: four save-failure paths told the user a failed save was "safely backed up locally" without checking whether the local backup actually succeeded.
	- Fixed (partial): added `vitest` + Testing Library to the repo (previously no component/rendering test coverage existed) and a `useStableCallback` hook, with a regression test, so the 17 callback props the map canvas passes into the marker/cable-line layers have a stable identity. Does not yet memoize `JointMapManager`'s ~800-property render-context object — see [[Active Bugs]].
	- Drafted, not deployed: `firestore.rules`/`storage.rules` changes locking the `assetChangeLogs` collection to Cloud-Function-only access and adding a size/type allowlist to the `asset-uploads` Storage path. Needs review before deploy.

