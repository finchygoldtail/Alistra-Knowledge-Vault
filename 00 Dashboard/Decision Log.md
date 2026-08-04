---
title: Decision Log
type: decision-log
status: active
owner: Alistair
created: 2026-08-02
updated: 2026-08-04
tags: [decisions, architecture]
---

# Decision Log

## Decisions

| Date | Decision | Linked Note | Status |
| --- | --- | --- | --- |
| 2026-08-02 | Obsidian is the product and architecture knowledge base. | [[Alistra Dashboard]] | accepted |
| 2026-08-02 | GitHub remains the source-code repository. | [[GitHub Workflow]] | accepted |
| 2026-08-02 | AlistraGIS follows an API-first architecture. | [[Architecture Overview]] | accepted |
| 2026-08-02 | Codex is used for implementation tasks. | [[Codex Backlog]] | accepted |
| 2026-08-04 | Firestore/Storage security rules changes must always be drafted and reviewed as a diff, never blind-deployed, given the risk of locking out legitimate users or leaving a gap. | [[Security Overview]] | accepted |
| 2026-08-04 | Map assets are stored as shared per-business chunk documents (`mapAssets/main/chunks/*`), which blocks a clean Firestore-rules-level fix for role-based edit/delete restrictions — rules can't distinguish "add an asset" from "delete one" within the same chunk write. Real fix needs either a data model change or a Cloud Function write gateway (as already used for `assetChangeLogs`). | [[Permissions Model]] | needs decision |
| 2026-08-04 | Do not attempt to memoize `JointMapManager`'s render context or wrap the map render layers in `React.memo` until the component is decomposed — the context object is too large (~800 properties) to safely enumerate dependencies by hand, and the risk is a stale-closure bug in marker click handlers on a live app. | [[Main Map]] | accepted |

## Template

Use [[Architecture Decision Template]] for future decisions.

