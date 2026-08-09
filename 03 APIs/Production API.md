---
title: Production API
type: api
status: active
owner: Alistair
created: 2026-08-02
updated: 2026-08-09
tags: [api, production]
---

# Production API

Supports daily production capture, route progress and field uploads.

## Mobile completion operation

The existing daily production callable now accepts an explicit completion mode for the mobile selected-asset workflow. `partial` keeps the normal range/splice entry, while `full` derives the remaining work from existing production records and writes only uncovered route gaps or remaining splices.

The server derives the production team from the asset type, validates project/area and crew scope, prevents duplicate submissions with idempotency keys, records server identity/timestamps, writes the asset completion status with the production update, and emits an audit event with the previous amount, added amount and new total. Field roles are permitted only through this narrow operation; they do not gain map-editing or manager permissions.

## Related

- [[Daily Production]]
- [[Route Progress]]
- [[Mobile and Tablet Plan]]
- [[Reporting]]
