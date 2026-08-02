---
title: API Gateway
type: architecture
status: draft
owner: Alistair
created: 2026-08-02
updated: 2026-08-02
tags: [api, gateway]
---

# API Gateway

The API gateway is the front door for platform capabilities. It should expose consistent authentication, authorization, validation, logging and error behaviour across [[API Catalogue]].

## Responsibilities

- Validate Firebase identity tokens from [[Authentication]].
- Enforce role and tenant checks from [[Permissions Model]] and [[Multi-Tenant Architecture]].
- Route requests to domain APIs such as [[Production API]] and [[Audits API]].

