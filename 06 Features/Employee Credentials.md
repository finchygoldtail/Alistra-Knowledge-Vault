---
title: Employee Credentials
type: feature
status: live
owner: Alistair
created: 2026-08-07
updated: 2026-08-07
tags: [feature, field, compliance]
---

# Employee Credentials

Company-wide employee roster tracking accreditations/certifications and their renewal dates (CSCS cards, tickets, etc.), with an Excel bulk-upload template matching the app's existing template pattern.

Built 2026-08-07. Firestore: `businesses/{companyId}/employees/{employeeId}`, fully server-managed. Client module: `src/modules/employees/`. Surfaced as a new section inside the Manage Users admin panel (see [[Manage Users]]), not a full workspace tab — an administrative roster task, closer to the existing User Register than to an operational Management Dashboard view.

## Independent of login accounts

`Employee` is deliberately a separate entity from `AppUserProfile` (the Firebase Auth-backed login/role system):

- `linkedUserUid` is optional and never required — most field staff don't have (and don't need) an app login, but still need tracked credentials.
- Never bidirectionally synced. `AppUserProfile` stays authoritative for a login-holder's name/role; `Employee` stays authoritative only for what it alone owns (phone, credentials, employee number, depot).
- When `linkedUserUid` is set, the write is rejected server-side unless a profile doc actually exists at that UID — a cheap guard against pointing at a deleted/nonexistent account.

See [[Decision Log]] for the full reasoning.

## Access

Read is open to any signed-in user (matches every other register in the app). Register edits, deletes and recording a credential are Manager+ (`requireManagerOrAbove`) — not opened to Supervisor in this first version, since it's administrative record-keeping rather than the approve/resolve/sign-off scope Supervisor was given. See [[Role Matrix]].

## Related

- [[Manage Users]]
- [[Plant and Equipment]] — same Excel bulk-import pattern (`xlsx`, data sheet + Guidance sheet, per-row validate-and-skip-with-error).
- [[Role Matrix]]
