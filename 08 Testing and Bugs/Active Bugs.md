---
title: Active Bugs
type: bug-index
status: active
owner: Alistair
created: 2026-08-02
updated: 2026-08-07
tags: [bugs, testing]
---

# Active Bugs

Use [[Bug Report Template]] for each bug. Link confirmed implementation fixes to [[Codex Backlog]].

Items below came out of the 2026-08-07 `fibre-gis` re-audit, "Round 4" ([full report](https://claude.ai/code/artifact/324913d5-bfae-41d3-9094-57757b60385b)) — a re-verification of every item still open on 2026-08-06 plus a dedicated review of everything shipped since the 2026-08-05 audit (the Plant & Equipment/Vehicle/Crew/Work Pack batch and the Supervisor role/session enforcement/employee roster/QR checkout/Fleet tab/as-built generator batch). Result at the time of the audit: 0 Critical, 1 High, 10 Medium, 8 Low. 10 of 19 findings are now fixed (the High, 6 Medium, 3 Low) — see [[Completed Tasks]]. Remaining items are either accepted architecture, need a real design decision (rate limiting), or aren't code bugs at all (the `any`-typing tracking methodology, the thin-CRUD-wrapper convention) — this round is being closed out here.

## Bugs

### High

- [x] ~~Bulk import panels (Employees, Plant Equipment, Vehicles) make one Cloud Function call per row — and per credential — instead of a batched write.~~ Fixed: added `bulkUpsertCompanyEmployees`/`bulkUpsertCompanyPlantEquipment`/`bulkUpsertCompanyVehicles`, each committing the whole import in one Firestore batched write per callable invocation instead of the client looping per row.

### Medium

- [x] ~~`recordCompanyDocument` has no role gate at all — any "user"-role account can attach an unvalidated `downloadUrl` to any asset's compliance record.~~ Fixed, but not by adding a role gate (self-service document uploads by field users are intended). Instead added `isCompanyStoragePath`/`isCompanyStorageDownloadUrl` validation, mirroring the existing ticket-attachment pattern (`functions/src/index.ts`'s `isValidTicketAttachmentUrl`) — `storagePath`/`downloadUrl` must now actually reference a file inside the caller's own company's Storage tree, closing the phishing-URL angle without blocking legitimate self-service uploads. Also added server-side `category` validation against the known `DocumentCategory` union (closes the related Low below).
- [x] ~~`createdByUid` is spoofable on edits across four registers (employees, plant equipment, vehicles, crews).~~ Fixed: new `resolveCreationFields()` helper reads the existing document's `createdAt`/`createdByUid` server-side (when editing) instead of trusting the client's spread `...input` for these fields — falls back to "now"/the caller only for a genuinely new record.
- [x] ~~QR scanner restarts the camera on every scan attempt.~~ Fixed: wrapped `onScanned` in the existing `useStableCallback` hook (already used and tested for the same class of problem in `JointMapCanvas.tsx`) so the camera-acquisition effect no longer depends on a callback identity that changes every render.
- [x] ~~User Register Inspector's unsaved form edits are silently discarded whenever `loadUsers()` runs for an unrelated reason.~~ Fixed: the field-sync effect now keys off `selectedUserUid` (a stable primitive) instead of `selectedUser` (a new object every list refresh), so it only re-syncs when the admin actually switches which user is selected.
- [x] ~~Fleet tab's `Promise.all` masks which of the two calls failed.~~ Fixed: switched to `Promise.allSettled` so a failure on one source no longer discards data that already loaded fine from the other, and the error message now names which register failed. The unfiltered/uncached read-volume half of this finding is unchanged — no cheaper query shape exists today without an API change (`listCompanyPlantEquipment`'s fast-path needs both `locationType` and `locationRefId`).
- [x] ~~`listCompanyCrews` writes an audit-log entry on every plain read, and `CrewPicker` re-fetches uncached from four drawers.~~ Fixed both: removed the audit-log write from the list callable (matches its siblings), and added a module-level 60s TTL cache + in-flight dedup to `CrewPicker.tsx`, shared across every instance regardless of which drawer mounted it.
- [x] ~~`firestore.indexes.json`'s `packs` composite index has no query behind it.~~ Fixed: removed the unused index entry.
- [x] ~~`stampUserSession` doesn't validate the caller belongs to the target `businessId`.~~ Fixed after re-tracing `resolveStorageContext`'s admin-exemption logic more carefully than the first pass: platform admins (the only role that legitimately switches business context — `canSwitchBusiness` is super_admin-only) are already exempted from the same-company check, so routing through `resolveStorageContext` doesn't actually risk that flow. Kept the existing `snapshot.exists` guard as a second check even after that, so an admin without a real membership doc at the target company still can't create a stray profile stub there.
- [ ] No rate limiting anywhere in `functions/src` — systemic, pre-existing since 2026-08-05, needs a real design decision (serverless-safe rate limiting isn't a quick fix), not attempted in this pass.
- [ ] Any business member can read (not write) any other member's assets/photos/employees/etc. — accepted architectural gap since 2026-08-04, not something to "fix" without a scoped ownership-model change.

### Low

- [x] ~~Document `category` field accepted with no server-side validation against the known category union.~~ Fixed alongside the `recordCompanyDocument` Medium above.
- [x] ~~`VehicleQrLabel` shows "Generating label…" indefinitely on a QR-encoding failure instead of a distinct error state.~~ Fixed, and applied the same fix to `PlantEquipmentQrLabel.tsx` (the file this was copied from, same bug) for consistency.
- [x] ~~`stampUserSession` failures are only `console.warn`'d.~~ Fixed: one automatic retry (covers a transient network blip, the most likely real cause), and a `console.error` with both failure details if it still fails twice — still deliberately non-blocking, doesn't interrupt sign-in.
- [ ] `listCompanyCrews`/`listCompanyDocumentsByCategory` use a fixed `.limit(500)` with no cursor pagination escape hatch — unlikely to matter at realistic scale, not fixed.
- [ ] `any`-typing baseline needs re-measuring on a consistent grep pattern — a tracking-methodology issue, not a code fix.
- [ ] `react-hooks/exhaustive-deps`/`set-state-in-effect` warnings: 55, map subsystem flat at 26 — scattered across many unrelated files, not a targeted fix; left for a dedicated lint-cleanup pass if wanted. Stale leftover git worktree at `.claude/worktrees/kind-goldstine-dbc83a/` still needs deleting (repo hygiene, unrelated to code).
- [ ] Oversized files: `JointMapManager.tsx` now 3,431 lines — a decomposition project, not something to attempt inside a bug-fix pass.
- [ ] Thin CRUD wrapper duplication across `src/modules/*` — confirmed a stable, accepted convention, not actually a problem.

