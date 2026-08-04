---
title: Active Bugs
type: bug-index
status: active
owner: Alistair
created: 2026-08-02
updated: 2026-08-04
tags: [bugs, testing]
---

# Active Bugs

Use [[Bug Report Template]] for each bug. Link confirmed implementation fixes to [[Codex Backlog]].

Items below came out of the 2026-08-04 `fibre-gis` audit ([full report](https://claude.ai/code/artifact/4eb9344d-8be3-4a04-9c47-9b31f275de3c)); see [[Completed Tasks]] for what was already fixed in that pass.

## Bugs

### High

- [ ] **Role-based edit/delete restrictions are UI-only, not enforced in Firestore rules.** A logged-in field engineer can bypass the app's role gates via devtools and directly delete/rewrite map assets for their business. Not a simple rules patch: map assets live in shared per-business chunk documents (`mapAssets/main/chunks/*`), so Firestore rules can't distinguish "add an asset" from "delete one" within the same document write. Needs either a data model change or a Cloud Function write gateway (mirroring the pattern already used for `assetChangeLogs`). See [[Permissions Model]], [[Role Matrix]], [[Security Overview]].
- [ ] **`JointMapManager`'s render context (`mapCanvasContext`) is rebuilt on every render.** ~800 properties across an ~830-line object literal; too large to safely memoize by hand without first decomposing the 4,207-line `JointMapManager.tsx`. Callback identity for the marker/cable-line layers is now stabilised (2026-08-04 fix), but the context object itself, and full `React.memo` on the render layers, remain open.

### Medium

- [ ] Every asset "view" (not just edits) fires an uncapped Firestore write, via two separate undebounced implementations.
- [ ] Any business member can read/write any other user's assets/photos — no per-asset ownership boundary below "member of this business."
- [ ] Photo/document uploads use non-resumable `uploadBytes`; a dropped connection restarts the whole upload from scratch instead of resuming.
- [ ] `AreaPolygonsLayer` has no viewport culling, unlike the other map layers.
- [ ] Failed loads of project homes fail silently — looks identical to "no homes recorded yet," risking duplicate re-entry.
- [ ] `any` typing is concentrated in the highest-risk code (map rendering, Firestore data mapping) — 2,500+ occurrences repo-wide, not evenly spread.
- [ ] Ten files are 2,000–4,200 lines, mixing data-fetching, business logic and rendering. `JointMapManager.tsx` (4,207 lines) is the largest and the root blocker for the two High items above.

### Low

- [ ] `react-hooks/exhaustive-deps` / `set-state-in-effect` lint warnings are concentrated in map and offline-save code — worth a manual pass, most likely spot for a real stale-closure bug among the lint noise.
- [ ] Audit-photo retry state is held only in memory; lost if the tab is backgrounded and reclaimed mid-retry.
- [ ] Production log removal has no retry affordance on failure (user has to manually repeat the action).
- [ ] Duplicated thin CRUD wrapper pattern repeated across domain modules in `src/modules/*`.

