---
title: Licensing Options
type: legal
status: draft
owner: Alistair
created: 2026-08-02
updated: 2026-09-05
tags: [legal, licensing]
---

# Licensing Options

## The technical shape this needs to wrap

The licence engine (`functions/src/api/companyLicence.ts`) already enforces, per company: a plan tier (`trial` / `subscription` / `enterprise`), a lifecycle status (`pending_setup` / `trial` / `active` / `expired` / `suspended` / `cancelled`), a seat cap (`maxUsers`, counted excluding AlistraGIS's own platform staff), an optional project cap (`maxProjects`), and a per-module feature list (`enabledFeatures` — map, overview, assets, audits, reports, commercial, operations, workpacks, hands). See [[Pricing Models]] for how these map to sellable tiers.

Whatever licence document gets signed needs to record real values for all of the above per customer — not just "a licence" in the abstract. [[Legal Pack Index]]'s version-control section already asks each signed contract to record "number and type of licensed users"; that maps directly to `maxUsers` and `enabledFeatures` above, but [[02 Software and SaaS Licence Agreement]] doesn't yet reference this technical model explicitly — worth adding when it's next reviewed, so the legal document and the enforced licence engine can't drift apart.

## Hosted vs. client-hosted use

- **Hosted use** (the only model live today): AlistraGIS operates the Firebase/GCP infrastructure; the customer's data sits in AlistraGIS's multi-tenant Firestore, isolated by `businessId`. See [[Hosting Options]].
- **Client-hosted use**: architecturally supported (a Postgres/PostGIS backend exists per storage profile), but not live for any customer — offering this today would be selling something not yet operational. Don't offer it as available now; it's a real near-term capability, not vapourware, but it needs the gap in [[Hosting Options]] closed first.

## Maintenance, upgrades and API access

- Maintenance/upgrade terms should match [[Maintenance and Upgrades]] and [[03 Service Level Agreement]] rather than being redefined here a third time.
- API access terms depend on which of the two things in [[API Buyout]] is actually being sold — hosted API access for a customer's own integrations, versus a source/IP licence. These need different clauses; don't conflate them in one licence document.

## Related

- [[Pricing Models]]
- [[Intellectual Property]]
- [[Data Ownership]]
- [[GDPR Responsibilities]]
- [[02 Software and SaaS Licence Agreement]]
