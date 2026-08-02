---
title: Multi-Tenant Architecture
type: architecture
status: draft
owner: Alistair
created: 2026-08-02
updated: 2026-08-02
tags: [multi-tenant, companies, projects]
---

# Multi-Tenant Architecture

AlistraGIS supports multiple companies and multiple projects. Every sensitive record should be scoped by tenant and project where applicable.

## Requirements

- Company-level user management through [[Manage Users]].
- Project-level access for map, production, audit and reporting data.
- Tenant-aware API enforcement through [[API Gateway]] and [[API Security]].

