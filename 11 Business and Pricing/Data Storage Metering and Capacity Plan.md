---
title: AlistraGIS Data Storage, Metering and Capacity Plan
type: business-architecture
status: working-plan
owner: Alistair
created: 2026-09-09
updated: 2026-09-09
tags: [data, storage, firebase, gcp, aws, azure, pricing, metering, capacity, hosting]
related: ["[[Client Pricing Pack]]", "[[Hosting Options]]", "[[15 Hosting and Data Responsibility Schedule]]", "[[Data Retention Schedule]]", "[[Subprocessor Register]]"]
---

# AlistraGIS Data Storage, Metering and Capacity Plan

> **Purpose:** define how AlistraGIS measures, stores, reports and commercially manages customer data across Firebase/Google Cloud, AWS and Microsoft Azure. This is a working commercial/technical plan. Provider prices and regions must be verified at quote/provisioning time before contractual commitments are made.

## 1. Objectives

AlistraGIS must be able to answer, for every customer and every month:

1. Which provider is storing the customer's data?
2. Which region is used?
3. How much active data is stored now?
4. What was average and peak storage during the month?
5. How much new data was uploaded this month?
6. How much data was downloaded/transferred out this month?
7. How much storage is database data, files/photos, backups and archive?
8. Which projects/areas are using the storage?
9. What is the customer's contracted storage allowance?
10. What is the projected usage in 30, 90 and 365 days?
11. What is the underlying provider cost?
12. What is AlistraGIS billing the customer?
13. Is the customer approaching a limit or creating an unexpected cost risk?

Data usage must therefore become a first-class company/project metric rather than an invisible cloud bill.

## 2. Data categories to meter separately

### 2.1 Structured application/database data

Examples:

- companies/tenants;
- users, roles and permissions;
- projects/areas;
- map assets and geometry;
- topology;
- production records;
- surveys;
- PIA/permit data;
- audits/QA;
- commercial records;
- work packs;
- management/crew/vehicle/equipment records;
- support/privacy workflow metadata;
- audit/change logs.

For Firebase this primarily means Firestore. For AWS/Azure customer-hosted architecture this is expected to move toward PostgreSQL/PostGIS where supported.

### 2.2 Object/file storage

Examples:

- photos;
- evidence images;
- PDFs;
- drawings;
- exported reports;
- imported spreadsheets;
- job packs;
- documents;
- employee credential documents;
- customer uploads;
- generated handover packs.

For Firebase/GCP this is Firebase/Google Cloud Storage. For AWS this is S3. For Azure this is Blob Storage.

### 2.3 Backups and versions

Meter separately from customer active data:

- Firestore PITR/backups;
- database snapshots;
- Storage/S3/Blob versions;
- backup mirrors;
- customer exit backup;
- disaster-recovery copies.

Standard backup footprint should normally be treated as an AlistraGIS operating cost rather than inflating the customer's visible active-storage figure. Extended retention or bespoke backup requirements can be separately priced.

### 2.4 Archive data

Historical/read-only projects should eventually be capable of using a lower-cost storage class:

- Google Cloud Nearline/Coldline/Archive;
- AWS S3 Intelligent-Tiering/IA/Glacier classes;
- Azure Cool/Cold/Archive tiers.

Do not commercially promise reduced archive rates until lifecycle movement and retrieval behaviour are technically implemented and tested.

### 2.5 Logs and telemetry

Track separately:

- application logs;
- security events;
- infrastructure/provider logs;
- API usage;
- audit trails;
- error/diagnostic data.

Logs can grow unexpectedly and must have retention limits and budget alerts.

## 3. Provider profiles

## 3.1 Firebase / Google Cloud — current production default

**Current status:** production-supported AlistraGIS-managed model.

Target service allocation:

| Function | Service |
|---|---|
| Identity | Firebase Authentication |
| Structured/realtime data | Cloud Firestore |
| Files/photos/documents | Firebase Storage / Google Cloud Storage |
| Backend | Cloud Functions / Google Cloud services |
| Secrets | Secret Manager |
| Backups | Firestore backup/PITR + object-storage backup/versioning controls |
| Frontend | Vercel, separately metered/managed |

Commercial cost drivers include:

- Firestore stored GiB;
- Firestore document reads/writes/deletes/index activity;
- Firestore network egress;
- Cloud Storage GB-month;
- storage operations;
- outbound network traffic;
- backup/PITR footprint;
- Cloud Functions/runtime use;
- logs.

Firebase's own free quotas must **not** be treated as customer entitlements because quotas apply at provider/project level and can be shared across tenants. AlistraGIS customer allowances are contractual allowances independent of provider promotional/free tiers.

**Region target:** UK/London (`europe-west2`) where the selected service supports it and where the deployment has been technically verified. Existing Vault evidence says Firestore is documented in `europe-west2`, but Storage/backup locations must still be verified before promising UK-only residency.

## 3.2 AWS — customer-specific/dedicated target architecture

**Current status:** architecture path exists but is not yet a general production toggle.

Target service allocation:

| Function | Proposed AWS service |
|---|---|
| Structured/geospatial data | Amazon RDS for PostgreSQL/PostGIS or approved managed PostgreSQL |
| Files/photos/documents | Amazon S3 |
| Secrets | AWS Secrets Manager |
| Monitoring | CloudWatch |
| Backups | RDS/AWS Backup + S3 versioning/lifecycle as approved |
| Identity | Existing AlistraGIS identity model unless a customer-specific identity integration is separately implemented |

Preferred UK region for UK-resident deployments: **Europe (London), `eu-west-2`**, subject to every required service being available and the customer's requirements.

AWS cost drivers include:

- S3 GB-month by storage class;
- PUT/GET/list and lifecycle requests;
- internet/cross-region transfer;
- PostgreSQL compute;
- database storage/IO;
- snapshots/backups;
- monitoring/logging;
- private networking/security services if requested.

Customer-owned AWS deployments should normally have AWS charge the customer directly. AlistraGIS charges implementation/integration/support under the commercial agreement.

## 3.3 Microsoft Azure — customer-specific/dedicated target architecture

**Current status:** architecture path exists but is not yet a general production toggle.

Target service allocation:

| Function | Proposed Azure service |
|---|---|
| Structured/geospatial data | Azure Database for PostgreSQL Flexible Server + PostGIS where approved |
| Files/photos/documents | Azure Blob Storage |
| Secrets | Azure Key Vault |
| Monitoring | Azure Monitor / Log Analytics as scoped |
| Backups | PostgreSQL backup + Blob versioning/lifecycle as approved |
| Identity | Existing AlistraGIS identity model; Microsoft Entra integration is a separate feature unless implemented |

Preferred UK region for UK-resident deployments: **UK South**, subject to required service availability and contractual verification.

Azure cost drivers include:

- Blob GB-month;
- Hot/Cool/Cold/Archive tier;
- LRS/ZRS/GRS or other redundancy selection;
- read/write/list operations;
- data retrieval and outbound transfer;
- PostgreSQL compute/storage/IO;
- backups;
- monitoring/logging;
- private endpoints/networking where requested.

Customer-owned Azure deployments should normally have Microsoft charge the customer directly. AlistraGIS charges implementation/integration/support under the commercial agreement.

## 4. Commercial storage allowances — working proposal

The current Core GIS Platform already includes a working **100 GB** pooled customer storage allowance. This plan refines how that should work.

### 4.1 Standard AlistraGIS-managed shared hosting

| Contracted active storage | Monthly storage add-on above Core | Position |
|---|---:|---|
| Up to 100 GB | Included | Core allowance |
| Up to 250 GB | +£60/month | Small photo/evidence growth |
| Up to 500 GB | +£125/month | Medium operational deployment |
| Up to 1 TB | +£250/month | Large field/evidence deployment |
| Up to 2 TB | +£450/month | Large regional customer |
| Up to 5 TB | +£950/month | Enterprise data tier |
| Over 5 TB | Bespoke quote | Provider/design review required |

All prices are working commercial figures, exclusive of VAT, and require margin validation before public publication.

### 4.2 What counts toward contracted active storage

Count:

- customer uploaded files/photos/documents;
- generated customer files retained in the live service;
- logical active application/database data;
- active project geometry/asset data;
- customer-specific retained exports where stored in the platform.

Do not normally count toward the customer's active-storage meter:

- standard AlistraGIS backup copies within the standard backup policy;
- temporary processing files that are deleted automatically;
- Supplier platform code/assets;
- Supplier security/operational logs, unless a customer requests bespoke long retention;
- provider indexing/metadata overhead that the customer cannot directly control.

AlistraGIS must still meter these excluded items internally because they affect provider cost and margin.

## 5. Monthly data-transfer/egress model

Storage capacity and monthly data movement are different cost drivers and must not be mixed together.

### Included allowance

Working proposal for standard shared hosting:

- first **100 GB/month outbound customer data transfer** included;
- inbound customer uploads are not separately charged under normal use, but uploaded files count toward stored capacity;
- internal provider traffic must be designed to avoid unnecessary cross-region charges.

### Working outbound overage

- above 100 GB/month: **£0.15 per additional GB** as a working shared-hosting rate;
- above 2 TB/month outbound: review/Enterprise quote or provider pass-through model;
- unusually expensive destination, cross-region or third-party network costs may be passed through where the Order Form permits.

Before publishing the fixed £/GB rate, validate it against the production region/provider and target margin.

## 6. Database operations/API usage

Do not initially invoice ordinary customers for every database read/write operation. That would make pricing difficult to understand.

Instead:

- meter reads/writes/deletes/API calls internally;
- include ordinary application usage under fair-use rules;
- create alerts for abnormal usage;
- use rate limiting/abuse controls;
- move genuinely high-volume integrations to a separate API/Enterprise usage schedule.

The internal dashboard should show estimated provider cost for database operations even when no customer line-item is generated.

## 7. Backup and retention pricing

### Standard

Standard Supplier-managed backup/recovery policy is included in the platform/hosting fee, subject to the approved retention schedule and SLA.

### Extended retention

Where a customer contractually requires longer retention, legal hold, extra replicas or bespoke backup:

- price separately after calculating active footprint and provider class;
- record backup region;
- record retention period;
- record recovery/retrieval target;
- do not imply that Archive/Glacier data is instantly retrievable unless the selected tier supports that.

Working placeholder for simple extended backup capacity: **from £25 per additional 100 GB/month**, subject to provider and recovery requirement. High-availability/geo-redundant solutions are bespoke.

## 8. Customer-hosted AWS/Azure data charging

For a customer-owned cloud account:

- customer pays AWS/Azure/database/storage/network bill directly;
- AlistraGIS should **still meter and display** storage and bandwidth usage;
- no normal AlistraGIS per-GB storage surcharge is required unless the contract says AlistraGIS manages or resells the infrastructure;
- AlistraGIS retains the existing implementation/activation and monthly integration/support charge;
- bespoke managed backup, monitoring, DR and cloud administration can be separately quoted.

This avoids AlistraGIS taking uncontrolled cloud-cost risk while still giving the customer a single operational usage dashboard.

## 9. Monthly usage record — required schema

Create one immutable monthly usage record per company, plus optional per-project breakdown.

Suggested logical fields:

```text
companyId
billingMonth
provider                firebase | aws | azure | other
hostingModel             alistra_shared | alistra_dedicated | customer_hosted
region
contractedStorageGb
activeStorageGbStart
activeStorageGbAverage
activeStorageGbPeak
activeStorageGbEnd
databaseLogicalGb
objectStorageGb
archiveStorageGb
backupStorageGbInternal
uploadsGbMonth
outboundGbMonth
fileCount
newFilesMonth
deletedFilesMonth
databaseReadsMonth
databaseWritesMonth
apiRequestsMonth
providerEstimatedCost
customerStorageCharge
customerEgressCharge
otherInfrastructureCharge
forecast30DayGb
forecast90DayGb
forecast365DayGb
calculatedAt
sourceStatus              measured | estimated | partial
```

Keep raw provider cost data restricted to authorised management/commercial users. Customer-facing usage can show consumption and contracted limits without exposing AlistraGIS margin unless desired.

## 10. Per-project/area attribution

Every uploaded object and significant database dataset should be attributable to:

- company;
- project/area where applicable;
- module/source;
- uploader/creator where appropriate;
- created date;
- data category;
- retention class.

Management must be able to see a table such as:

| Project | Active data | Photos | Documents | Database | Monthly uploads | Monthly outbound | 30-day growth |
|---|---:|---:|---:|---:|---:|---:|---:|
| Area 1 | 82 GB | 68 GB | 8 GB | 6 GB | 14 GB | 22 GB | +9% |
| Area 2 | 41 GB | 30 GB | 6 GB | 5 GB | 4 GB | 9 GB | +3% |

This makes data cost attributable to real work rather than only to a whole-company bucket.

## 11. Customer Data Usage dashboard

Add a **Data Usage** panel to Management/Company settings.

### Headline cards

- Provider: Firebase / AWS / Azure;
- Hosting model;
- Region;
- Storage used: `386 GB / 500 GB`;
- Storage utilisation: `77.2%`;
- Uploads this month;
- outbound transfer this month;
- database size;
- files/photos size;
- backup footprint (management only where appropriate);
- estimated month-end storage;
- projected provider cost (management only);
- next storage tier and cost impact.

### Graphs

- daily storage GB for last 90 days;
- monthly upload GB;
- monthly outbound GB;
- storage by project;
- storage by data type;
- provider cost trend;
- forecast capacity.

### Forecasting

Calculate:

- average daily growth over 30 days;
- average daily growth over 90 days;
- projected date to reach 85%, 100% and next storage tier;
- projected 12-month data footprint.

Do not forecast from only one or two abnormal upload days without showing confidence/quality warnings.

## 12. Threshold and notification policy

| Usage | Action |
|---|---|
| 70% | Informational dashboard notice |
| 85% | Warning to company billing/admin contact + AlistraGIS management |
| 95% | Commercial/storage review; forecast next tier |
| 100% | Begin contractual overage/grace process; do not silently create unlimited cost |
| 110% | Critical review; require upgrade/action unless temporary approved burst |

Do **not** automatically block safety/QA evidence uploads solely because storage has reached 100% unless the contract and product workflow explicitly allow it. A controlled grace/overage process is safer than causing field data loss.

## 13. Cost and margin controls

For AlistraGIS-managed hosting, management needs both customer usage and supplier cost.

Track monthly:

```text
Provider storage cost
+ database operations cost
+ network/egress cost
+ backup cost
+ compute/functions cost attributable where practical
+ logging/monitoring cost
= estimated infrastructure cost

Customer recurring platform/hosting/data fees
- estimated infrastructure cost
= gross infrastructure contribution before labour/support
```

Set internal cost alerts at provider/account and tenant-estimate level.

Suggested initial alerts:

- provider bill +25% month-on-month;
- one tenant responsible for >20% of shared infrastructure cost;
- outbound traffic >2x prior 30-day average;
- storage growth >20% in seven days;
- unexpected cross-region traffic;
- backup footprint >2x active data without approved reason;
- logging cost >configured percentage of tenant revenue.

## 14. Provider selection rules

### Use Firebase/GCP when

- standard AlistraGIS-managed multi-tenant deployment;
- customer accepts Supplier-managed cloud;
- current production architecture is appropriate;
- no unsupported customer-owned database requirement exists.

### Consider AWS when

- customer requires AWS tenancy/account;
- customer requires S3/PostgreSQL/PostGIS architecture;
- procurement/security policy prefers AWS;
- UK London `eu-west-2` services satisfy requirements;
- customer-specific acceptance checklist passes.

### Consider Azure when

- customer is Microsoft/Azure standardised;
- customer requires Azure tenancy/subscription;
- Azure Blob + PostgreSQL/PostGIS architecture meets requirements;
- UK South services satisfy requirements;
- customer-specific acceptance checklist passes.

Provider choice should never be made solely on headline £/GB storage price. Database compute, operations, egress, resilience, backups, private networking, monitoring, support and engineering effort can dominate the storage-only number.

## 15. Data residency and provider-change controls

Every signed Order should record:

- provider;
- cloud-account owner;
- production region;
- database region;
- object-storage region;
- backup region;
- allowed support/access locations where contractually relevant;
- transfer mechanism where required;
- whether customer approval is required before a material provider/region change.

The platform must not label a tenant "UK-hosted" solely because its primary database is in a UK region while object storage, backups, logs or another processor is elsewhere.

## 16. Data lifecycle

Suggested lifecycle states:

`ACTIVE -> READ_ONLY -> ARCHIVE_ELIGIBLE -> ARCHIVED -> DELETE_PENDING -> DELETED`

Lifecycle is controlled by the approved retention schedule and customer contract, not merely by storage cost.

Future automation should support:

- dry-run report before deletion/tiering;
- legal hold override;
- customer/project retention policy;
- data export before termination where required;
- audit record of lifecycle action;
- provider-specific storage-class transition.

## 17. Billing logic

For shared AlistraGIS-managed hosting:

```text
Monthly Recurring Data Charge
= contracted storage tier fee
+ outbound data overage
+ approved extended backup/retention fee
+ bespoke provider/network pass-through
```

Do not bill from raw provider invoice line items unless the customer contract explicitly uses pass-through billing.

For customer-hosted AWS/Azure:

```text
Customer cloud bill -> paid directly by Customer
AlistraGIS charge -> integration/support/managed-service fee
Usage dashboard -> still records GB, bandwidth and forecast
```

## 18. Quote and Order Form fields to add

Every Order should include:

- hosting provider;
- hosting model;
- region;
- included/contracted active storage GB;
- included outbound GB/month;
- outbound overage method/rate;
- backup retention;
- archive requirement;
- data-residency requirement;
- customer-hosted cloud account owner;
- responsibility for cloud bill;
- expected initial import size;
- expected monthly growth;
- expected photo/evidence volume;
- expected API/integration volume if material;
- notification contacts for capacity/billing alerts.

## 19. Implementation phases

### Phase 1 — Meter current Firebase production

1. Measure per-company object-storage bytes.
2. Measure logical Firestore/database footprint per company using an auditable approximation/export method.
3. Measure uploads/downloads where technically available.
4. Create daily usage snapshots.
5. Aggregate into monthly company usage records.
6. Add management-only cost fields.
7. Add 70/85/95/100% alerts.

### Phase 2 — Customer dashboard

1. Add Data Usage page/cards.
2. Add per-project breakdown.
3. Add 30/90/365-day forecasts.
4. Add storage-tier recommendation.
5. Add CSV/PDF usage export if useful for account reviews.

### Phase 3 — Commercial automation

1. Store contracted storage tier on company licence/order metadata.
2. Calculate egress overage.
3. Feed approved usage charges into Commercial/billing workflow.
4. Require commercial approval before automatic tier changes initially.
5. Add monthly customer usage statement.

### Phase 4 — AWS/Azure provider adapters

1. Normalise provider metrics to the same internal usage schema.
2. Read S3/Blob/PostgreSQL metrics from approved customer deployment.
3. Preserve provider-specific raw cost data separately.
4. Validate London/UK South region and backup configuration.
5. Pass customer-hosted acceptance/security/restore tests before production.

### Phase 5 — Lifecycle optimisation

1. Archive-eligible classification.
2. Storage-class transitions.
3. Extended retention pricing.
4. Archive retrieval workflow.
5. Cost optimisation recommendations.

## 20. Current commercial recommendation

Keep the customer proposition easy to understand:

**Licence + modules + users + projects + hosting + storage/data usage + support.**

For most customers, sell a fixed active-storage tier and include ordinary database/API usage rather than presenting a complicated cloud-provider invoice.

For customer-owned AWS/Azure, let the customer pay the provider directly while AlistraGIS charges activation and ongoing integration/support. This gives AlistraGIS predictable margin and removes the risk of financing a large enterprise customer's cloud consumption.

## 21. Provider-pricing notes checked 9 September 2026

Provider pricing is variable and must be rechecked before publication/quote.

- Firebase/Firestore charges can include stored data, reads/writes/deletes, indexes, bandwidth and backup/PITR usage. Firebase Cloud Storage uses Google Cloud Storage pricing for modern buckets.
- Google Cloud Storage pricing varies by region, storage class, operations and network use.
- Amazon S3 pricing varies by storage class, stored volume, requests, retrieval and data transfer; AWS currently provides the first 100 GB/month of internet data transfer out free across most AWS services/regions, but this is a provider-level allowance and must not be promised as a per-customer AlistraGIS entitlement.
- Azure Blob pricing varies by GB-month, access tier, redundancy, transactions, retrieval and data transfer.

Use live provider calculators/account billing data for actual infrastructure estimates rather than hard-coding today's provider unit prices into the customer contract.

## 22. Decisions still required

- [ ] approve or change the proposed storage tier prices;
- [ ] approve the proposed 100 GB/month outbound allowance;
- [ ] approve or change the working £0.15/GB outbound overage;
- [ ] decide whether client-facing dashboard shows actual £ charge or only usage/allowance;
- [ ] define standard backup retention once legal/technical retention values are approved;
- [ ] decide whether archived projects continue consuming active storage until archive tiering is implemented;
- [ ] validate measurement approach for logical Firestore data per tenant;
- [ ] add billing/order/licence fields;
- [ ] implement provider metrics adapters;
- [ ] validate gross margins using real production usage after first pilot.
