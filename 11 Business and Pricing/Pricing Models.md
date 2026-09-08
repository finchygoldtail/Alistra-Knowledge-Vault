---
title: Pricing Models
type: business
status: working-commercial-model
owner: Alistair
created: 2026-08-02
updated: 2026-09-08
tags: [pricing, business]
related: ["[[Client Pricing Pack]]", "[[Hosting Options]]", "[[13 Client Framework Agreement]]", "[[14 Client Order Form and Service Schedule]]"]
---

# Pricing Models

The detailed working price book is now maintained in [[Client Pricing Pack]]. This page records the commercial logic behind it and how it maps to the licence engine.

## What the product already meters

The licence system tracks, per company:

- **Plan tier** (`licenceType`): `trial`, `subscription`, or `enterprise`.
- **Status lifecycle**: `pending_setup` → `trial` → `active` → `expired` / `suspended` / `cancelled`.
- **Trial period**: default **7 days** (`DEFAULT_TRIAL_DAYS`).
- **Seats**: `maxUsers` caps active users; active users consume seats except `super_admin` platform/support accounts where excluded by current logic.
- **Projects**: `maxProjects` optionally caps project count.
- **Feature modules** (`enabledFeatures`): `map`, `overview`, `assets`, `audits`, `reports`, `commercial`, `operations`, `workpacks`, `hands`.
- **Storage provider**: Firebase is the current production-supported option. Azure/AWS route toward the shared PostGIS architecture but remain customer-specific/fail-closed until provisioned and validated — see [[Hosting Options]].

This supports pricing across **core platform + modules + seats + projects + hosting + support/services** without needing a separate product for each customer.

## Current working commercial structure

### Core Platform

**£1,250/month excl. VAT**

Working package includes:

- Core GIS/Map + Overview + Assets;
- first 10 active users;
- first 5 active projects;
- standard AlistraGIS-managed shared hosting;
- Standard Support.

### Optional modules

| Module | Monthly working price |
|---|---:|
| QA & Audits | £350 |
| Reports & Handover Reporting | £250 |
| Commercial | £550 |
| Operations & Production | £450 |
| Work Packs | £350 |
| Health & Safety / HANDS | £300 |

Full current module set including Core: **£3,500/month before additional seats/hosting/support**.

### Seat bands

First 10 users are included in Core. For seats above 10:

| Total contracted users | Price per additional user/month |
|---|---:|
| 11–25 | £30 |
| 26–50 | £25 |
| 51–100 | £20 |
| 101–250 | £15 |
| 251+ | Enterprise quote |

### Project capacity

First 5 active projects included. Working rate for additional active projects: **£75/project/month**.

### Hosting

- AlistraGIS-managed shared hosting: included in Core, subject to the Order Form allowance.
- Dedicated Supplier-managed environment/data layer: setup from **£2,500** plus **£850/month**.
- Customer-selected/customer-hosted Azure/AWS/Postgres/PostGIS: activation from **£4,500** plus **£450/month** platform integration/support; customer pays its own infrastructure unless otherwise agreed.

### Support

- Standard: included.
- Priority: **£500/month**.
- Enterprise/Extended: from **£1,250/month**.

### Implementation/services

Detailed rates are in [[Client Pricing Pack]]. Working rates include standard onboarding at **£1,500**, training from **£650–£750/day**, migration at **£850/day**, and integration/bespoke engineering at **£900/day**.

## Contract mechanism

Do not amend the master licence for every commercial variation.

Use:

1. [[13 Client Framework Agreement]] as the reusable master agreement;
2. [[14 Client Order Form and Service Schedule]] to record modules, users, projects, hosting, support and fees; and
3. [[15 Hosting and Data Responsibility Schedule]] to allocate hosting/security/backup responsibilities.

Only the signed Order Form makes a quoted price contractually binding.

## Annual billing

Current working incentive: **10% discount** on approved recurring software/module/seat fees where paid annually in advance. Do not automatically discount pass-through infrastructure, one-off work, usage overages or professional services.

## Important product-packaging rule

Some customer-facing capabilities such as Maintenance, PIA/Permits, advanced Topology, Management APIs and FRIDAY AI may not yet have independent licence flags. Until they do, price them within an enforceable existing module or as a bespoke Enterprise add-on clearly described in the Order Form.

## Related

- [[Client Pricing Pack]] — detailed quote book and examples.
- [[Hosting Options]] — technical hosting reality.
- [[13 Client Framework Agreement]]
- [[14 Client Order Form and Service Schedule]]
- [[15 Hosting and Data Responsibility Schedule]]
- [[Maintenance and Upgrades]]
- [[API Buyout]]
- [[Licensing Options]]
