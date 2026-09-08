---
title: AlistraGIS Hosting and Data Responsibility Schedule
status: draft-for-solicitor-and-technical-review
updated: 2026-09-08
owner: Alistair
related: ["[[13 Client Framework Agreement]]", "[[14 Client Order Form and Service Schedule]]", "[[Hosting Options]]", "[[Subprocessor Register]]", "[[DPA Requirements]]", "[[Backup and Recovery]]"]
---

# Hosting and Data Responsibility Schedule

> This schedule allocates operational responsibilities according to the hosting model selected in the Client Order Form. It must match the actual deployed architecture. Do not promise a hosting mode, residency position, backup capability or recovery target that has not been technically verified.

## 1. Supported hosting models

### Model A — AlistraGIS-managed shared hosting

Current production-supported default.

Typical stack as documented at 8 September 2026:

- Vercel frontend delivery;
- Firebase Authentication;
- Google Cloud / Firebase Cloud Functions;
- Firestore;
- Firebase/Google Cloud Storage;
- Secret Manager and associated platform services.

The Supplier selects and manages the infrastructure/subprocessors, subject to the DPA, subprocessor register and verified production configuration.

### Model B — AlistraGIS-managed dedicated environment/data layer

Optional commercial model where a customer requires additional logical or infrastructure separation. The exact architecture must be designed and quoted before sale.

A dedicated environment does not automatically imply UK-only data residency, private networking, a dedicated application codebase or customer-owned cloud. The Order Form must state exactly what is dedicated.

### Model C — Customer-selected / customer-hosted cloud or server

Intended for customers requiring their own Azure, AWS, PostgreSQL/PostGIS or other approved environment.

As at 8 September 2026 this model is **not an instant production toggle**. The codebase contains a Postgres repository path and Azure/AWS storage profiles, but customer-specific database connectivity, secrets and production validation are still required before activation.

The Supplier may refuse or defer an unsupported architecture, version or provider.

## 2. Responsibility matrix

| Responsibility | Model A — AlistraGIS managed | Model B — Supplier dedicated | Model C — Customer selected/hosted |
|---|---|---|---|
| Application code | Supplier | Supplier | Supplier unless separately licensed otherwise |
| Frontend deployment | Supplier | Supplier | Supplier or as Order Form states |
| Database service selection | Supplier | Supplier | Customer + Supplier approval |
| Cloud account owner | Supplier | Supplier unless stated | Customer |
| Infrastructure bill | Supplier, recovered through fees | Supplier, recovered through fees | Customer directly unless agreed otherwise |
| Database configuration | Supplier | Supplier | Shared responsibility per Order |
| Infrastructure admin credentials | Supplier controlled | Supplier controlled | Customer controlled; Supplier gets least-privilege support access where agreed |
| User identity/role management | Shared: platform controls + Customer admins | Shared | Shared |
| Customer source data accuracy | Customer | Customer | Customer |
| Application security fixes | Supplier | Supplier | Supplier for application components |
| Cloud/IaaS patching | Provider/Supplier | Provider/Supplier | Customer/provider unless managed-service scope says otherwise |
| Network/firewall/VPC | Supplier/provider | Supplier/provider | Customer unless explicitly managed by Supplier |
| Secrets storage | Supplier | Supplier | Shared; customer-owned credentials remain Customer responsibility unless managed service agreed |
| Backup policy | Supplier | Supplier | Customer by default unless Supplier managed backup purchased |
| Restore execution | Supplier | Supplier | Customer infrastructure + Supplier application support as allocated |
| Availability of customer cloud | N/A/customer not owner | N/A/customer not owner | Customer/provider risk |
| Data export | Supplier-supported product export | Supplier-supported product export | Shared depending on data plane |
| Infrastructure deletion on exit | Supplier | Supplier | Customer for Customer-owned cloud; Supplier deletes Supplier-held copies per DPA |
| Subprocessor selection | Supplier | Supplier | Customer for Customer cloud + Supplier for Supplier services |
| Data residency verification | Supplier | Supplier | Shared; Customer must confirm chosen region/account |
| DPA/transfer documentation | Supplier for Supplier processors | Supplier | Shared according to role chain |
| Logging/monitoring | Supplier/provider | Supplier/provider | Shared per deployment |
| Penetration/security testing of Supplier app | Supplier | Supplier | Supplier; Customer tests Customer infrastructure |
| Disaster-recovery test | Supplier | Supplier | Shared and scope-specific |

## 3. Data residency

The Order Form must record verified regions for the deployed customer environment.

Do not state that all AlistraGIS data is UK-only or EU-only unless every relevant service, storage location, backup, log, support route and subprocessor used for that customer has been checked.

The current Vault records Firestore production in `europe-west2` while some Storage/backup components have previously been documented in `US-EAST1`; live settings must be verified before contractual residency commitments are made.

## 4. Backups and recovery

### Supplier-managed environments

The current recovery evidence includes Firestore point-in-time recovery, scheduled backups and tested isolated restore capability. The specific production commitments offered to a customer must be stated in the SLA and must not exceed tested capability.

The Order Form should specify:

- backup owner;
- backup frequency;
- retention/expiry approach;
- target RPO/RTO if contractually promised;
- restoration scope;
- exclusions;
- whether uploaded files/object storage are covered by the same recovery process.

### Customer-hosted environments

Unless the Order Form says otherwise, the Customer is responsible for:

- database/provider backup configuration;
- storage replication/versioning;
- infrastructure snapshots;
- backup access controls;
- cloud-account continuity;
- infrastructure-side restore capability.

The Supplier may provide application-level recovery assistance at the agreed professional-services/support rate.

## 5. Security ownership

### Supplier responsibilities

Where within Supplier control:

- secure development and code maintenance;
- application authentication/authorisation logic;
- tenant/business scoping;
- Firestore/Storage/API rules in Supplier-managed environments;
- secret handling for Supplier credentials;
- vulnerability remediation;
- application audit controls;
- incident handling for Supplier systems.

### Customer responsibilities

- authorised user list;
- role assignment and periodic review;
- endpoint/device security;
- account hygiene and prompt leaver removal;
- lawful and accurate Customer Data;
- customer-controlled cloud administrators;
- customer network/firewall/security configuration where applicable;
- secure handling of Customer-owned credentials;
- notification of suspected compromise.

## 6. Data protection role interaction

The hosting model does not by itself decide controller/processor status.

The intended default remains:

- Customer normally controller for its own project/workforce/evidence personal data;
- AlistraGIS normally processor for that data where it hosts/processes it to supply the service;
- AlistraGIS controller for its own account administration, service security, billing/licensing, support and supplier-management data where it determines purposes and means.

Customer-hosted infrastructure may change the processor/subprocessor chain but does not automatically remove AlistraGIS from UK GDPR obligations if the service still accesses or processes personal data.

## 7. Subprocessors

The Supplier maintains [[Subprocessor Register]].

For Supplier-managed hosting, subprocessors may include providers for cloud hosting, authentication, storage, frontend deployment, mapping/geocoding and optional AI functionality.

For Customer-hosted deployments, the Customer's chosen cloud/provider may be directly contracted by the Customer. The Order Form/DPA must identify whether that provider is the Customer's processor, the Supplier's subprocessor or part of another lawful arrangement.

## 8. Customer-selected infrastructure acceptance checklist

Before Model C can go live:

- [ ] provider/account is approved;
- [ ] supported database version/service confirmed;
- [ ] network route/connectivity confirmed;
- [ ] secrets integration implemented;
- [ ] least-privilege Supplier access agreed;
- [ ] region/data-residency verified;
- [ ] backup owner and restore method confirmed;
- [ ] monitoring/logging responsibility confirmed;
- [ ] performance/load test passed;
- [ ] tenant-isolation/security regression passed;
- [ ] export and termination process tested;
- [ ] DPA/subprocessor/transfer wording updated;
- [ ] SLA exclusions/targets updated;
- [ ] implementation fee accepted;
- [ ] production fail-closed guard removed only for the approved customer/configuration.

## 9. Exit responsibilities

### Supplier-managed

The Supplier provides the supported export/exit path stated in the Order Form and applies the approved retention/deletion process to Supplier-managed systems and backups.

### Customer-hosted

The Customer is responsible for Customer-owned infrastructure shutdown, credential revocation, cloud-resource deletion and provider account retention after the Supplier has completed its agreed export/application-side exit tasks.

The Supplier remains responsible for deleting or lawfully retaining any Supplier-held copies according to the DPA and retention schedule.

## 10. Commercial consequences

Hosting choice may affect:

- one-off provisioning/engineering fee;
- monthly hosting/management fee;
- Customer direct infrastructure costs;
- support tier;
- SLA scope;
- backup/recovery responsibilities;
- data-residency commitments;
- security testing effort;
- migration/exit cost.

The applicable charges are recorded in [[Client Pricing Pack]] and the signed Order Form.

## 11. Professional review points

Solicitor/privacy review should confirm:

- controller/processor/subprocessor wording for each hosting model;
- transfer wording and residency commitments;
- liability split for Customer-controlled infrastructure;
- backup/data-loss exclusions and caps;
- incident notification responsibilities; and
- termination/deletion wording for customer-owned cloud environments.
