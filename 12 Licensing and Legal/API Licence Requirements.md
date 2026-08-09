---
status: draft
updated: 2026-08-08
stage: 19
related: ["[[API Security Assessment 2026-08-08]]", "[[API Security]]", "[[API Catalogue]]", "[[DPA Requirements]]", "[[02 Software and SaaS Licence Agreement]]"]
---

# API Licence Requirements

Stage 19 of the commercial go-live programme. This document defines requirements for an AlistraGIS API licence/addendum. It is not final legal wording and must be reviewed by a solicitor before commercial use.

## Files reviewed for this stage

| File | Why it was reviewed | Result |
|---|---|---|
| `fibre-gis/docs/API.md` | Current public/documented HTTP API | Confirms production API is the Firebase HTTPS Function named `api` and uses `Authorization: Bearer <firebase-id-token>`. |
| `fibre-gis/functions/src/storage/storageHttpApi.ts` | Actual API auth/routing/roles | Confirms bearer token verification, tenant context resolution, licence gate, map/work-pack role gates and safe HTTP errors (`storageHttpApi.ts:224`-`345`, `633`-`805`). |
| `fibre-gis/functions/src/api/companyLicence.ts` | Licence enforcement | Confirms expired/suspended licences are blocked and seat limits are enforced. |
| `Alistra Knowledge Vault/09 Security and Permissions/API Security Assessment 2026-08-08.md` | Previous API security inventory | Used as the security baseline and open-gap list. |
| `Alistra Knowledge Vault/12 Licensing and Legal/02 Software and SaaS Licence Agreement.md` | Existing commercial licence | API addendum should attach to this rather than replace it. |

## Scope

The API licence should cover customer, partner or third-party use of AlistraGIS APIs, including:

- Firebase callable functions used by the app;
- the documented HTTP API in `fibre-gis/docs/API.md`;
- any future customer/partner integrations;
- build-partner access where applicable;
- API credentials, authentication tokens and account-based access.

## Authentication and Credentials

The licence should require:

- authenticated API access only;
- Firebase ID token or approved service credential as applicable;
- credentials tied to a named customer, business, user, build partner or integration;
- no credential sharing between organisations;
- immediate notification of suspected compromise;
- AlistraGIS right to rotate, suspend or revoke credentials.

## Permitted Use

Permitted use should be limited to:

- integrating the customer's own authorised systems with its own AlistraGIS tenant;
- reading or updating data the customer is authorised to access;
- operational reporting, project workflows and approved automation;
- use within agreed licence modules and active subscription status.

## Prohibited Use

The licence should prohibit:

- accessing or attempting to access another customer's data;
- bypassing role, tenant or project controls;
- scraping, bulk extraction or replication beyond agreed export rights;
- reselling or redistributing API access;
- using API output to build a competing platform without written permission;
- reverse engineering, probing or stress testing outside an authorised test scope;
- automated abuse, denial of service, credential stuffing or rate-limit evasion;
- uploading unlawful, malicious or unsafe content.

## Rate Limits and Abuse Controls

The API terms should reserve the right to impose:

- per-user, per-tenant and per-token rate limits;
- request-size caps;
- file-size and MIME/content restrictions;
- AI usage limits;
- export/import caps;
- temporary throttling during incidents or abuse;
- suspension where usage risks security, stability or excessive cost.

Exact limits may be documented in an order form or technical API documentation and may change for security or platform-protection reasons.

## Data Ownership and IP

The licence should state:

- customer retains ownership of its customer data;
- AlistraGIS retains platform/source-code/IP ownership;
- API schemas, documentation and SDKs remain AlistraGIS IP unless otherwise agreed;
- API use does not grant source-code rights or database redistribution rights;
- aggregated/non-identifying operational metrics may be used for service improvement if covered by the privacy/DPA terms.

## Security Responsibilities

Customers/integrators should be responsible for:

- protecting tokens and credentials;
- using HTTPS only;
- implementing least privilege in their own systems;
- not embedding server credentials in frontend/public code;
- validating their own users before calling AlistraGIS APIs;
- promptly removing access for leavers;
- reporting suspected vulnerabilities privately.

AlistraGIS should be responsible for platform-side:

- tenant isolation;
- server-side authorisation;
- secure Firestore/Storage/API rules;
- audit logging of sensitive API actions;
- reasonable monitoring and incident response.

## Caching and Data Copies

The licence should define:

- whether customer systems may cache API responses;
- maximum cache duration;
- deletion obligations after contract termination;
- treatment of audit/security logs;
- prohibition on retaining another party's data after access ends.

## Availability and Changes

The API licence should avoid over-promising. It should state:

- API availability is governed by the SLA/order form;
- breaking changes require reasonable notice except for urgent security fixes;
- deprecated endpoints may be withdrawn after notice;
- emergency restrictions may be applied to protect security or stability.

## Termination and Revocation

AlistraGIS should be able to revoke or suspend API access for:

- non-payment or expired licence;
- suspected compromise;
- breach of acceptable-use/security terms;
- excessive or harmful usage;
- customer termination;
- legal or regulatory requirement.

Customer data export/return on termination should follow the SaaS agreement, DPA and [[Data Retention Schedule]].

## Open Legal / Product Items

| ID | Requirement | Status |
|---|---|---|
| API-LIC-01 | Decide whether API access is included in standard plans or sold as a separate module | Required |
| API-LIC-02 | Define baseline rate limits and overage/abuse handling | Required |
| API-LIC-03 | Confirm whether third-party customer apps are allowed and under what approval process | Required |
| API-LIC-04 | Add audit logging to any API export paths that are not currently server-side logged | Required |
| API-LIC-05 | Solicitor review of final API terms/addendum | Required |

## Current Stage Result

API licence requirements are defined for solicitor drafting/review. They are not yet executable contract terms.
