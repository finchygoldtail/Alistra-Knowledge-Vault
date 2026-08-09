---
title: API Security
type: security
status: live
owner: Alistair
created: 2026-08-02
updated: 2026-08-08
tags: [security, api]
---

# API Security

API security validates identity, role, company scope and project scope before domain operations are allowed.

## Requirements

- Verify Firebase Authentication identity.
- Enforce [[Permissions Model]].
- Enforce tenant rules from [[Multi-Tenant Architecture]].
- Record sensitive actions in [[Audit Logging]].

## Status

A full endpoint-by-endpoint audit ran 2026-08-08 — see [[API Security Assessment 2026-08-08]]. All 124 Cloud Functions read in full. Result: 120 of 124 already enforced this correctly; 4 didn't (a real cross-tenant PII leak via live GPS location data, plus a permit-extension endpoint reachable by any company). Fixed the same day, not yet deployed.

