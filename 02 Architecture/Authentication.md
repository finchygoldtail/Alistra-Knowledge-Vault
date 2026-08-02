---
title: Authentication
type: architecture
status: draft
owner: Alistair
created: 2026-08-02
updated: 2026-08-02
tags: [auth, firebase]
---

# Authentication

AlistraGIS uses Firebase Authentication with Google and email authentication.

## Requirements

- Support Google sign-in and email sign-in.
- Connect authenticated users to company and project access in [[Permissions Model]].
- Support future login restrictions in [[Concurrent Login Control]].

