---
title: Hosting Options
type: business
status: draft
owner: Alistair
created: 2026-08-02
updated: 2026-09-05
tags: [hosting, pricing]
---

# Hosting Options

## What's actually deployable today

**AlistraGIS-managed hosting (the only option live in production):**

- Frontend: static build hosted on **Vercel**, deployed on every push to `main` (`git push origin main` triggers the Vercel build — Firebase Hosting is not the serving path, only a redirect).
- Backend: **Firebase** — Cloud Functions (`europe-west2`), Firestore, Firebase Auth, Firebase Storage, Secret Manager.
- This is the only storage provider actually enabled: `functions/src/storage/storageRouter.ts` throws `STORAGE_PROVIDER_UNSUPPORTED` for any company profile set to `azure` or `aws` unless a live bundle is wired in, and today none is — see `docs/STORAGE_PROVIDER_PHASE_1.md`, which documents this as **deliberately fail-closed**, not a bug.

**Client-hosted / dedicated storage (built, not yet enabled):**

- A parallel `PostgresAssetRepository` exists (`functions/src/storage/postgresAssetRepository.ts`) that both an `azure` and an `aws` storage profile route to — same code, different profile config, not two separate implementations.
- The Postgres schema already has company/area-scoped tables (including an `area_id` column on map assets — not yet fully wired end-to-end, see `functions/src/storage/postgresMappers.ts`).
- Activating this for a real customer requires: a live client database connection, a secret provider for that customer's credentials, and removing the fail-closed guard for that specific company. None of this is a pricing decision alone — it's real engineering work, currently paused (`POSTGIS_FIREBASE_HANDOVER.md`, repo root, describes the migration as in-progress with known gaps).

## Hosting model comparison

| Model | Who owns the data plane | What's real today | Cost driver |
|---|---|---|---|
| AlistraGIS-managed (Firebase) | AlistraGIS's own Firebase project, multi-tenant | **Live for every current customer** | AlistraGIS's own Firebase/GCP bill, scales with all tenants combined |
| Client-hosted (Azure/AWS + PostGIS) | Customer's own cloud account/database | Code exists, fail-closed, no live customer on it | Customer's own infra cost, plus AlistraGIS engineering time to activate and support it |

Anyone asking for "our own database" or "we want this in our own Azure tenant" today is asking for something the architecture is built towards but hasn't been switched on for a paying customer yet — say that plainly rather than implying it's a flip of a setting.

## Related

- [[Pricing Models]]
- [[Vercel Deployment]]
- [[Firebase Infrastructure]]
- [[Client Hosted Deployment]]
- [[Subprocessor Register]] — confirms Vercel/Firebase/GCP as the actual current subprocessors; Azure/AWS listed there as conditional/not-yet-enabled, matching this page.
