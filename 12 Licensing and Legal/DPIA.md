---
status: draft-for-professional-review
updated: 2026-09-07
stage: 16
related: ["[[03 GDPR Data Register]]", "[[Data Retention Schedule]]", "[[Subprocessor Register]]", "[[FRIDAY Security Model]]", "[[API Security Assessment 2026-08-08]]", "[[Security Overview]]", "[[Stage 20 Backup Implementation]]", "[[Stage 21 Restore Test]]", "[[Data Breach and Incident Response]]"]
---

# Data Protection Impact Assessment

Stage 16 of the commercial go-live programme. This is an engineering-led DPIA draft for AlistraGIS / `fibre-gis`, based on source-code and vault evidence. It is not legal advice and does not decide, by itself, whether a DPIA is legally mandatory. It records the facts and risks for review by a solicitor, DPO or customer privacy lead.

## Scope

AlistraGIS is a B2B infrastructure GIS and operations platform, currently focused on fibre/telecommunications with planned expansion into water, gas, electricity/power, renewables and wireless point-to-point/line-of-sight infrastructure. It stores customer-controlled operational records including map assets, projects, work packs, employee/vehicle/plant records, files/photos, support tickets, audit events and limited licence metadata. FRIDAY AI is currently designed as a read-only assistant operating within the caller's permissions.

The documented platform uses Firebase/GCP backend services and Vercel frontend hosting.

## Controller / Processor Position

Working assumption for professional review: AlistraGIS is usually a processor for customer-controlled project, workforce and evidence data, while acting as controller for its own platform administration, security, billing/licence, support and vendor-management operations. This must be confirmed in the DPA and customer contract and may differ for specific features or deployment models.

## Data and Processing Risks

| Area | Risk | Current controls/evidence | Residual risk / action |
|---|---|---|---|
| Tenant isolation | Cross-customer access could expose commercially sensitive infrastructure and personal data | Firestore rule protections, business-membership helper patterns, API/security remediation and security regression evidence are documented | Complete broader black-box tenant-isolation/security regression before commercial go-live and repeat after material architecture changes |
| Photographs/evidence | Site photos may include people, vehicles, homes/private property | Business-scoped Storage and upload controls | Retention enforcement and user guidance remain required |
| Workforce activity | Work packs, audit logs, vehicles/plant and credentials can reveal who did what and when | Role controls, audit logging; unused live GPS removed | Review access/minimisation and customer retention choices |
| Location/geocoding | Tile/geocoding providers receive browser IP plus tile/coordinate requests | Only requested map/geocode data is sent; no app secret deliberately sent | Disclose/review providers and commercial terms; consider contracted/self-hosted alternatives where needed |
| FRIDAY AI | Prompt/tool context may include customer/personal data | Read-only tool design, caller scoping, no application retention of prompt/reply text | NVIDIA DPA/processing region still needs confirmation before customer enablement; reassess on RAG/chat history/write tools |
| Audit logs | User identifiers/actions can become excessive if retained indefinitely | Server-side logging and identity hardening documented | No approved expiry/archive/minimisation enforcement yet |
| Support tickets | Free text may contain account/security/personal information | Narrower access controls than ordinary collections | Retention/archive/delete process still required |
| Backups | Deleted data may remain in protected backup cycles | Firestore PITR, daily backup with 30-day retention, daily append-only Storage mirror and successful isolated restore test now evidenced | Append-only Storage mirror requires approved retention enforcement; customer/privacy wording must explain backup cycle |
| Privileged accounts | Admin/developer compromise can expose multiple records | Role gates/auth/security hardening documented | Final monitoring, incident ownership and operational verification required |
| New utility sectors | Water/gas/power/renewables data can increase operational consequence of inaccurate records | Existing contract draft requires independent operational verification | Reassess DPIA/security/contract risk when each sector becomes production scope |

## Necessity and Proportionality

The core processing is necessary for infrastructure GIS/project operations, but AlistraGIS should avoid collecting categories not needed for a defined feature. Removal of unused live GPS is the preferred privacy pattern: remove unnecessary collection rather than governing it indefinitely.

Proportionality before commercial pilot depends particularly on approved retention/enforcement, subprocessor/transfer confirmation, DSAR procedures, incident response and security regression testing.

## High-Risk / Change-Trigger Features

| Feature | DPIA position |
|---|---|
| Live GPS/worker tracking | Removed. Any reintroduction requires fresh DPIA/privacy/employment review before implementation. |
| Site/property photographs | Potential personal data by context; requires guidance, access control and retention/deletion. |
| Employee/credential records | Workforce/compliance information; role allocation and retention responsibilities must be explicit. |
| FRIDAY AI | Current design is read-only/non-retentive in app logs, but provider terms/region must be settled before commercial use. |
| AI chat history/RAG/document search | Not covered as a settled production feature; requires reassessment before enablement. |
| Write-capable AI/agents | Requires a fresh DPIA/security/control assessment before production use. |
| New utility sectors | Water, gas, power/electricity, renewables and wireless LOS should each trigger review of data categories, operational consequence and customer contract wording before production launch. |

## Backup and recovery update — 7 September 2026

The original August DPIA described backup/restore as incomplete. That statement is now superseded by later programme evidence:

- [[Stage 20 Backup Implementation]] records Firestore PITR, daily backups with 30-day retention and a verified daily append-only Storage mirror as live.
- [[Stage 21 Restore Test]] records an isolated Firestore restore passing on 11 August 2026 in 627.893 seconds, with production left unchanged and representative data/index/security checks completed.
- Residual recovery work concerns wider frontend rollback, selective Storage restoration, application cutover/failover and deputy ownership under the disaster-recovery programme.

## Preliminary Outcome

**DPIA prepared for professional review; not represented as legally approved or complete.**

No single identified issue in this engineering assessment automatically establishes that the service cannot be piloted. However, the commercial programme should not mark privacy readiness complete until the P1 retention, subprocessor/transfer, DSAR, incident-response and legal-role questions are closed or formally accepted for a controlled pilot.

## Required Actions

| ID | Action | Priority | Status |
|---|---|---|---|
| DPIA-01 | Legal/privacy review of controller/processor split and whether a formal DPIA is legally required | P1 | Required |
| DPIA-02 | Approve and enforce [[Data Retention Schedule]] | P1 | Required |
| DPIA-03 | Confirm [[Subprocessor Register]] DPA/region/transfer status and update privacy notice | P1 | Required |
| DPIA-04 | Complete DSAR request register and deletion/export/minimisation runbook | P1 | Required |
| DPIA-05 | Backup/isolated restore proof | P1 | Complete — see Stages 20/21 |
| DPIA-06 | Complete remaining wider DR failover/cutover exercises and assign deputy | P1 | Required |
| DPIA-07 | Run/refresh tenant-isolation/security regression across Firestore, Storage, APIs and Cloud Functions before go-live | P1 | Required |
| DPIA-08 | Operationalise [[Data Breach and Incident Response]] and run tabletop exercise | P1 | Required |
| DPIA-09 | Reassess before live tracking, AI history/RAG, write-capable AI, or production launch of additional utility sectors | P1 | Ongoing trigger |

## Professional review questions

1. Is a DPIA mandatory for the current product/service and intended B2B customers?
2. Is the proposed controller/processor allocation correct, including support/security/licensing data?
3. Are the residual risks and mitigations proportionate for a controlled pilot?
4. Does US-EAST1 Storage processing require additional transfer/customer documentation or architecture change for intended UK customers?
5. What retention/minimisation decisions should be made for audit logs, change logs, support tickets, workforce records and backups?
6. What changes should automatically trigger a new DPIA rather than an ordinary review?
