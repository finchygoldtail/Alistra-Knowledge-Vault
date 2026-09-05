---
title: Pricing Models
type: business
status: draft
owner: Alistair
created: 2026-08-02
updated: 2026-09-05
tags: [pricing, business]
---

# Pricing Models

> Grounded in what the licence engine (`functions/src/api/companyLicence.ts`) actually enforces today, not aspirational. Figures marked **[SET PRICE]** are illustrative placeholders — real numbers are a business decision, not something to infer from the code.

## What the product already meters

The licence system already tracks, per company:

- **Plan tier** (`licenceType`): `trial`, `subscription`, or `enterprise` — three tiers already exist in code, not two.
- **Status lifecycle**: `pending_setup` → `trial` → `active` → `expired` / `suspended` / `cancelled`. A trial defaults to **7 days** (`DEFAULT_TRIAL_DAYS`) and expires automatically.
- **Seats**: `maxUsers` caps active users; a seat is consumed by every active user **except `super_admin`** — AlistraGIS's own platform staff sitting inside a customer's tenant for support never counts against the customer's seat count or bill. This is already enforced (`assertCompanyHasSeatCapacity` blocks adding a user once `seatsUsed >= maxUsers`).
- **Projects**: `maxProjects` optionally caps how many project areas a company can run.
- **Feature modules** (`enabledFeatures`): map, overview, assets, audits, reports, commercial, operations, workpacks, hands — each can be independently licensed on or off per company. A company can be sold a subset.
- **Storage provider**: Firebase is live in production today; AWS and Azure (via a shared PostGIS backend) exist in code but are deliberately fail-closed until a real client database connection is provisioned — see [[Hosting Options]].

This means a real pricing model can already be built along three independent axes without any new engineering: **seats**, **feature modules**, and **plan tier** (trial/subscription/enterprise). Per-area/per-project pricing is also structurally possible (`maxProjects` exists) but not yet tied to anything commercial.

## Candidate structure

| Tier | Seats | Modules | Support | Illustrative price |
|---|---|---|---|---|
| Trial | Uncapped (or a small cap) | Full or a demo subset | Self-serve | Free, 7 days, auto-expires |
| Subscription | Per-seat, metered by `maxUsers` | Chosen subset of the 9 modules | Standard | **[SET PRICE]** /seat/month |
| Enterprise | Custom/uncapped | All modules, including anything not yet module-gated (e.g. FRIDAY AI) | Named support, custom SLA | **[SET PRICE]**, negotiated |

Because `enabledFeatures` is already per-company, a genuine "good/better/best" module bundle is a licence-document change, not a code change — worth deciding the actual bundles (which modules sit in which tier) alongside the price itself.

## Related

- [[Hosting Options]] — how the storage-provider choice affects cost and what's actually deployable today.
- [[Maintenance and Upgrades]]
- [[API Buyout]]
- [[Licensing Options]] — the legal shape this pricing structure needs to be wrapped in.
- [[02 Software and SaaS Licence Agreement]] — where seat counts, price and renewal terms get recorded per signed customer.
