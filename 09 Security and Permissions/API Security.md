---
title: API Security
type: security
status: draft
owner: Alistair
created: 2026-08-02
updated: 2026-08-02
tags: [security, api]
---

# API Security

API security validates identity, role, company scope and project scope before domain operations are allowed.

## Requirements

- Verify Firebase Authentication identity.
- Enforce [[Permissions Model]].
- Enforce tenant rules from [[Multi-Tenant Architecture]].
- Record sensitive actions in [[Audit Logging]].

