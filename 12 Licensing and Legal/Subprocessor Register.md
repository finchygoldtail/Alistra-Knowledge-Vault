---
status: draft
updated: 2026-08-08
stage: 15
related: ["[[03 GDPR Data Register]]", "[[Data Retention Schedule]]", "[[Firebase Infrastructure]]", "[[Vercel Deployment]]", "[[FRIDAY Security Model]]", "[[Privacy Notice and Website Legal Notices]]"]
---

# Subprocessor Register

Stage 15 of the commercial go-live programme. This register lists actual and conditional providers found in the `fibre-gis` codebase and vault. It should be reviewed against live account settings, contracts and DPAs before commercial use.

## Files reviewed for this stage

| File | Why it was reviewed | Result |
|---|---|---|
| `fibre-gis/src/firebase.ts` | Firebase project, Auth, Firestore, Storage and Functions setup | Confirms Firebase/GCP production project identifiers and browser SDK use. |
| `fibre-gis/functions/src/friday/fridayConfig.ts` and `friday/nvidiaClient.ts` | AI provider configuration | Confirms NVIDIA endpoint and `NVIDIA_API_KEY` Secret Manager pattern; OpenAI SDK is only the client library. |
| `fibre-gis/functions/src/index.ts` | Street Manager API integration | Confirms optional Street Manager permit extension path and stored request/response excerpts (`index.ts:674`-`789`). |
| `fibre-gis/src/config/mapTiles.ts` and `src/components/map/layers/FreeLeafletBaseLayer.tsx` | Mapping tile providers | Confirms CARTO/OpenStreetMap tile usage. |
| `fibre-gis/src/components/map/permits/permitLocationLookup.ts` | Reverse geocoding provider | Confirms Nominatim reverse geocoding call. |
| `fibre-gis/functions/src/storage/storageProfile.ts` and `storageProfileManagement.ts` | Optional storage providers | Confirms Azure/AWS profile support fields, but not production enablement. |
| `Alistra Knowledge Vault/10 Deployment and Infrastructure/Vercel Deployment.md` | Frontend hosting | Confirms Vercel serves `alistragis.com` and Firebase Hosting only redirects. |

## Confirmed Providers

| Provider | Purpose | Data processed | Location / region | Contract or DPA status | International transfer mechanism | Status |
|---|---|---|---|---|---|---|
| Google Firebase / Google Cloud Platform | Authentication, Firestore database, Firebase Storage, Cloud Functions, Secret Manager, platform logs | Account identifiers, names/emails, roles, project/customer data, files/photos, audit events, support tickets, FRIDAY safe audit events, possible platform request logs/IPs | App code uses `europe-west2`; actual Firebase/Auth/logging residency must be confirmed in console | Google Cloud/Firebase terms and DPA required | Google Cloud DPA/SCCs or UK addendum mechanism to confirm | Confirmed in code; contract settings require review |
| Vercel | Public frontend hosting for `alistragis.com` / `www.alistragis.uk` | Browser requests, IP addresses, device/browser metadata, static frontend delivery logs; no Firestore customer records stored in source code | Vercel region/settings not confirmed from repo | Vercel terms/DPA required | Vercel DPA/SCCs or UK addendum mechanism to confirm | Confirmed in vault deployment docs |
| GitHub | Source-code repository, CI/workflow integration, Vercel deployment trigger | Source code, commit metadata, developer identities; not intended to process customer production data | GitHub account/region not confirmed | GitHub terms/DPA required for business use | GitHub DPA/SCCs or UK addendum mechanism to confirm | Confirmed by repo workflow/vault; production-data handling should be prohibited |
| NVIDIA | FRIDAY AI completion endpoint when FRIDAY is enabled and paid/free allowance is available | User prompt text, server-supplied production summary returned by FRIDAY's read-only tool, model response metadata; app does not persist prompt/reply content | NVIDIA endpoint defaults to `https://integrate.api.nvidia.com/v1`; processing region not confirmed | NVIDIA AI/API terms and DPA required before customer use | NVIDIA transfer mechanism to confirm | Conditional active provider: code path exists, guarded by `FRIDAY_ENABLED` and `FRIDAY_ALLOW_PAID_AI` |
| CARTO / OpenStreetMap tile infrastructure | Basemap tile display via `https://basemaps.cartocdn.com/rastertiles/voyager/{z}/{x}/{y}.png` | User IP address, browser metadata, requested map tile coordinates/zoom; no authenticated app payload deliberately sent | Public CDN/service locations not confirmed | CARTO/OSM tile terms need review | Transfer mechanism not confirmed | Confirmed client-side dependency |
| OpenStreetMap Nominatim | Reverse geocoding for permit-location autofill via `https://nominatim.openstreetmap.org/reverse` | User IP address and selected latitude/longitude sent from browser | Public service locations not confirmed | Nominatim/OSM usage policy and privacy terms need review | Transfer mechanism not confirmed | Confirmed client-side dependency |

## Conditional / Optional Providers

| Provider | Trigger | Purpose | Data processed | Status |
|---|---|---|---|---|
| Microsoft Azure | Customer storage profile chooses `azure` | Optional PostgreSQL/PostGIS and Azure Blob style customer-dedicated/client-owned storage | Customer project/map/files data if enabled | Code supports profile validation, but production router indicates non-Firebase providers are not enabled for production operations yet; contract/DPA needed before activation |
| Amazon Web Services | Customer storage profile chooses `aws` | Optional PostgreSQL/PostGIS and S3 style customer-dedicated/client-owned storage | Customer project/map/files data if enabled | Code supports profile validation, but production router indicates AWS storage is not enabled for production operations yet; contract/DPA needed before activation |
| Street Manager API provider | `STREET_MANAGER_API_TOKEN`, `STREET_MANAGER_API_BASE_URL` and related env vars configured | Permit extension requests for enabled customer/business workflow | Permit number, works reference, dates, asset context, API response excerpts stored in `streetManagerPermitRequests` | Code path exists for Harrellicomms permit workflow; actual provider, DPA and data terms must be confirmed from env/contract |
| Google Maps | User clicks generated directions links | Opens external route/directions page for selected coordinates | Destination coordinate and user's Google/browser context after click | Not embedded processing by AlistraGIS; disclose as external link if used |

## Not Currently Processors For Production Customer Data

| Provider / tool | Reason |
|---|---|
| OpenAI | The `openai` npm SDK is used as a client library to call NVIDIA's OpenAI-compatible endpoint. No OpenAI API base URL or OpenAI service call was found in the active FRIDAY implementation. Reassess if the base URL or model provider changes. |
| Anthropic | Mentioned in the working process/assistant context, but no production app integration found in code. |
| Stripe / payment processor | No live payment-processing integration found in source during this review. Billing/licence metadata exists in Firestore, but no card/bank processing path was identified. |
| Sentry / PostHog / analytics providers | No production integration found in source during this review. |

## Required Actions

| ID | Requirement | Priority | Status |
|---|---|---|---|
| SUB-01 | Confirm Google Cloud/Firebase region, logging retention and DPA status in the console/account | P1 | Required |
| SUB-02 | Confirm Vercel team DPA, deployment region/log-retention settings and production domain ownership | P1 | Required |
| SUB-03 | Decide whether FRIDAY/NVIDIA is enabled for any pilot customer; if yes, confirm NVIDIA data processing terms before use | P1 | Required |
| SUB-04 | Review CARTO and Nominatim/OpenStreetMap terms for production/commercial tile and geocoding usage | P1 | Required |
| SUB-05 | Confirm the actual Street Manager API provider and contractual/data-processing basis before enabling permit-extension calls | P1 | Required |
| SUB-06 | Update [[Privacy Notice and Website Legal Notices]] from this register before publication | P1 | Required |

## Review Cycle

Review this register before any controlled commercial pilot, whenever a new provider is added, whenever FRIDAY/provider configuration changes, and at least annually once the product is live.
