---
status: draft
updated: 2026-08-08
stage: 16
related: ["[[03 GDPR Data Register]]", "[[Data Retention Schedule]]", "[[Subprocessor Register]]", "[[FRIDAY Security Model]]", "[[API Security Assessment 2026-08-08]]", "[[Security Overview]]"]
---

# Data Protection Impact Assessment

Stage 16 of the commercial go-live programme. This is an engineering-led DPIA draft for AlistraGIS / `fibre-gis`, based on the current source code and vault evidence. It is not legal advice and does not decide, by itself, whether a DPIA is legally mandatory. It records the facts and risks that a solicitor, DPO or customer privacy lead should review.

## Scope

AlistraGIS is a B2B telecommunications GIS and operations platform. It stores customer-controlled operational records for fibre projects, map assets, work packs, employee/vehicle/plant records, files/photos, support tickets, audit events and limited licence metadata. FRIDAY AI is a read-only assistant that can summarise production data within the caller's existing permissions.

The live product is `C:\Projects\fibre-gis`, deployed with Firebase/GCP backend services and Vercel frontend hosting.

## Files reviewed for this stage

| File | Why it was reviewed | Result |
|---|---|---|
| `Alistra Knowledge Vault/12 Licensing and Legal/03 GDPR Data Register.md` | Data categories and previous Stage 13 findings | Used as the primary input. |
| `fibre-gis/functions/src/index.ts` | Tickets, user deletion, company backup/delete, Street Manager and asset logs | Confirms support/free-text, permit API, manual deletion and backup-before-delete flows. |
| `fibre-gis/functions/src/friday/fridayCallables.ts` | AI processing and logging | Confirms FRIDAY is read-only, rate-limited, does not persist prompts/replies in app logs, and sends data to NVIDIA if enabled. |
| `fibre-gis/src/components/map/permits/permitLocationLookup.ts` | Geolocation/geocoding | Confirms coordinate-based Nominatim lookup. |
| `fibre-gis/src/config/mapTiles.ts` and `FreeLeafletBaseLayer.tsx` | Map tile exposure | Confirms map tile providers see tile/coordinate requests from browser clients. |
| `Alistra Knowledge Vault/09 Security and Permissions/API Security Assessment 2026-08-08.md` | Tenant isolation and API findings | Used for residual security-risk context. |

## Controller / Processor Position

Working assumption for review: AlistraGIS is usually a processor for customer-controlled project, workforce and evidence data, while acting as controller for its own platform administration, billing/licence and support operations. This must be confirmed in the DPA and customer contract.

## Data and Processing Risks

| Area | Risk | Current controls | Residual risk | Action |
|---|---|---|---|---|
| Tenant isolation | Cross-customer access to Firestore, Storage or Cloud Functions would expose commercially sensitive project data and personal data | Stage 2-4 work added/emulator-tested Firestore rule protections; API review found and fixed/deleted live-location BOLA paths; shared helper patterns enforce business membership | Wider black-box tenant isolation testing still required across APIs, Storage and UI flows | Complete Stage 30/31 regression and internal pen-test work before go-live |
| Photographs and audit evidence | Site photos may incidentally include people, vehicles, homes or private property | Storage is business-scoped; uploads have route/type/size controls from Stage 5; live-location feature was removed | Retention is not automated; users may upload unnecessary personal data | Add retention enforcement and user guidance for evidence uploads |
| Field-worker activity | Work packs, production logs, vehicle/plant check-outs and employee credentials can reveal who did what, where and when | Role-based access, server-side audit logging, no live GPS after Stage 13 cleanup | Audit and operational records are readable more broadly than strict privacy minimisation may require | Review audit/read access and retention with customers |
| Location/geocoding | Permit location lookup sends selected coordinates to Nominatim; map tiles reveal viewed areas to tile provider/CDN | Only selected coordinate/tile requests sent; no app secrets in those calls | External services receive IP plus coordinate/tile request data | Disclose providers; review commercial terms; consider self-hosted/paid providers if needed |
| FRIDAY AI | AI prompt could include personal/customer data; model output could leak data if tool scoping were weak | FRIDAY has one read-only tool, no caller-controlled business/project parameters, no retained prompt/reply text, no write capability, rate limits and paid-AI guard | NVIDIA processing terms/region not confirmed; future RAG/chat-history would change risk profile | Confirm NVIDIA DPA before enabling for customers; reassess on any AI capability expansion |
| Audit logs | Logs contain user identifiers and actions; unbounded logs can become excessive | Logs are server-stamped and server-write-only; identity forgery fixed; admin/user-management events added | No retention/archival job; read access may be wider than necessary | Implement Data Retention Schedule and review log read permissions |
| Support tickets | Tickets can contain account/security issues and free-text personal data | Ticket access is narrower than ordinary business collections; attachment URLs are constrained to same-business Storage | No deletion/retention workflow; sensitive user-provided text remains indefinitely | Add closed-ticket retention/archive/delete process |
| Backups | Deletion backups can preserve deleted personal data beyond the active system | `backupAndDeleteCompany` creates manifest backup before destructive delete | No backup expiry job found; access model and encryption evidence not fully documented | Complete backup/restore stages before go-live |
| Privileged accounts | Admin or platform-owner compromise could expose many records | Role gates, owner-email guard, MFA/auth hardening documented elsewhere | Admin login audit event not implemented; MFA status needs final operational confirmation | Finish auth hardening and monitoring |

## Necessity and Proportionality

The main processing is necessary for the product's purpose: managing fibre build/project operations and evidence. However, the platform must avoid collecting data it does not need. The Stage 13 removal of unused live GPS functions is the right privacy pattern: if a category is not operationally required, remove it rather than govern it indefinitely.

Proportionality depends on completing the remaining P1 controls: retention, subprocessor confirmation, DSAR procedure, incident response, backup/restore test, monitoring and security regression testing.

## High-Risk Features Reviewed

| Feature | DPIA note |
|---|---|
| Live GPS tracking | Removed from the codebase after confirming no UI integration. Reintroduction would require a fresh DPIA review before implementation. |
| Site/property photographs | Potential personal data by context; requires upload guidance, retention and deletion processes. |
| Employee/credential records | May include workforce compliance information; customers need clear role allocation and retention responsibility. |
| FRIDAY AI | Current implementation is read-only and non-retentive, but provider terms and customer notice must be settled before commercial use. |
| Street Manager permit extension | Sends permit/work-reference data to an external API if configured; provider and terms must be confirmed. |

## Preliminary Outcome

Current conclusion: **DPIA draft requires review; commercial pilot should not treat DPIA as complete until P1 actions are closed or accepted.**

No single remaining issue appears to force an automatic no-go if the pilot is controlled and customer terms are explicit, but the combination of unimplemented retention, incomplete subprocessor confirmation and untested backup/restore remains a commercial-readiness blocker under the programme's own gates.

## Required Actions

| ID | Action | Priority | Status |
|---|---|---|---|
| DPIA-01 | Legal/privacy review of controller/processor split and whether a formal DPIA is legally required | P1 | Required |
| DPIA-02 | Complete and enforce [[Data Retention Schedule]] | P1 | Required |
| DPIA-03 | Confirm [[Subprocessor Register]] contract/DPA status and update privacy notice | P1 | Required |
| DPIA-04 | Complete DSAR process and deletion/export runbook | P1 | Required |
| DPIA-05 | Complete backup, restore test and disaster recovery plan | P1 | Required |
| DPIA-06 | Run tenant-isolation/security regression tests across Firestore, Storage, APIs and Cloud Functions | P1 | Required |
| DPIA-07 | Reassess before adding live tracking, FRIDAY chat history, RAG/document search, or write-capable AI tools | P1 | Required |
