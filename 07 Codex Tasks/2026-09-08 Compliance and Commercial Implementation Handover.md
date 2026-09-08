---
title: Compliance and Commercial Implementation Handover
status: ready-for-codex
updated: 2026-09-08
owner: Alistair
related: ["[[16 UK Compliance Action Register 2026-09-08]]", "[[12 Data Protection Complaints Procedure]]", "[[Data Subject Rights Procedure]]", "[[13 Client Framework Agreement]]", "[[14 Client Order Form and Service Schedule]]", "[[Client Pricing Pack]]"]
---

# 2026-09-08 Compliance and Commercial Implementation Handover

## Objective

Implement the highest-priority product changes required to support the newly updated legal/commercial Vault without inventing legal retention periods, claiming unsupported hosting capability or adding unnecessary cookie banners.

## P1 — Data-protection complaint intake

Implement an admin/support workflow aligned with [[12 Data Protection Complaints Procedure]].

### Required behaviour

- Add support/privacy category: `Privacy / Data Protection Complaint`.
- Record:
  - complaint reference;
  - received timestamp;
  - acknowledgement timestamp;
  - customer/business/tenant;
  - requester/contact;
  - data subject if different;
  - controller/processor routing status;
  - owner;
  - status;
  - updates;
  - outcome;
  - closure timestamp;
  - linked DSAR/incident/ticket references.
- Add due/overdue indicator for the statutory 30-day acknowledgement requirement.
- Do not automatically send sensitive complaint detail to users outside the authorised privacy/admin group.
- Allow complaint status reporting/export for governance.
- Audit-log privileged complaint access and material state changes where appropriate.

### UX

Provide a clear route under support/help/privacy. Do not require a person to know specific legal terminology.

## P1 — DSAR/request register

Implement the minimum reliable tooling needed by [[Data Subject Rights Procedure]].

### Required fields

- request type;
- received date/time;
- requester/data subject;
- customer/business;
- identity/authority status;
- due date;
- clarification requested/date;
- extension used/reason;
- owner;
- search/export status;
- decision/outcome;
- linked complaint/incident;
- completion date.

### Deadline logic

- ordinary SAR deadline: one month;
- extension: up to two additional months where permitted;
- do not hardcode assumptions for non-SAR rights without a clearly documented rule;
- display deadline warnings rather than silently auto-closing requests.

### Search/export helper

Admin-only helper should locate, where relevant:

- Firebase Auth account;
- root/business user profiles;
- tickets/events;
- asset-change logs;
- audit events;
- employee/credential records;
- crew/vehicle/plant/work-pack references;
- files/photos metadata and references;
- AlistraGIS-controlled licence/support records.

Do not produce an unrestricted whole-tenant export to an ordinary user.

## P1 — Company website legal disclosure

The public website/app legal/footer area must be capable of showing:

- `Alistra GIS Ltd`;
- company number `17361925`;
- `Registered in England and Wales`;
- current registered-office address;
- legal/privacy contact route.

**Do not hardcode a guessed/private address.** Add a configuration value/place-holder gate if the approved public registered-office address has not yet been supplied. Publication cannot be marked complete until the actual Companies House address is inserted.

## P1 — Retention worker: dry-run first

Build configurable retention enforcement using the existing storage/data policy fields.

### Phase 1

- dry-run/report-only;
- list records/files that would be archived, anonymised or deleted by policy category;
- no destructive action;
- tenant-scoped and admin-only;
- audit execution/result;
- support exclusions/legal holds.

### Phase 2

Enable destructive enforcement only after approved policy values exist for each data category.

Do not assume `30 days` applies universally merely because backup lifecycle uses 30 days.

## P1 — Subprocessor/provider verification surface

Create a simple internal admin/compliance register or documentation checklist for:

- provider;
- service;
- contract/DPA verified date;
- production region;
- backup region;
- log retention;
- transfer mechanism/status;
- owner;
- review date.

This may initially remain Vault/manual rather than product UI if faster, but do not claim verification without account-level evidence.

## P1 — Contract/licence metadata

Ensure each customer company record can support or already exposes:

- Framework Agreement version/date;
- Order Form reference;
- selected modules;
- max users;
- max projects;
- hosting model;
- support tier;
- subscription start/end/renewal;
- pricing reference/plan;
- DPA version/status;
- customer commercial/technical/privacy contacts.

Use existing licence fields where possible. Do not duplicate truth unnecessarily.

## P2 — Quote/configurator screen

Create an admin-only quote builder based on [[Client Pricing Pack]] only after the commercial price table is approved.

Inputs:

- modules;
- seat count;
- projects;
- hosting model;
- support tier;
- onboarding/migration days;
- API/AI add-ons;
- monthly vs annual billing.

Outputs:

- monthly recurring charge;
- one-off charge;
- annual prepay calculation;
- first-year value;
- quote reference/version;
- printable/exportable quote summary.

Prices must be stored/configured centrally rather than copied across UI components.

## P2 — Hosting readiness guard

Customer-hosted Azure/AWS/PostGIS must remain unavailable for production selection unless the customer/environment passes the acceptance checklist in [[15 Hosting and Data Responsibility Schedule]].

Do not remove the fail-closed production guard globally.

Prefer per-customer/approved-environment enablement.

## P2 — Privacy/legal UI

Update legal/about screens to reflect the approved versions of:

- Privacy Notice;
- Cookie/Device Storage Notice;
- Data Protection Complaints route;
- company details;
- support/security contact.

Do not add a generic cookie banner unless a production audit confirms consent-requiring technology is present.

## Testing requirements

Before marking complete:

1. mock data-protection complaint received and acknowledged;
2. mock SAR due-date calculation and extension flow;
3. per-user locator tested against representative records;
4. ordinary user cannot access privacy complaint register;
5. cross-tenant complaint/DSAR access denied;
6. retention dry-run cannot delete data;
7. company legal footer displays configured data and no guessed address;
8. customer-hosted option remains fail-closed without approval;
9. quote maths unit tests cover all seat bands and annual discount;
10. pricing/config changes require privileged role.

## Do not do

- Do not invent final legal retention periods.
- Do not state that AlistraGIS has ISO 27001/Cyber Essentials certification unless actually achieved.
- Do not make UK-only data-residency claims without verified provider evidence.
- Do not deploy consent banners merely for appearance.
- Do not enable live GPS/worker tracking as part of this task.
- Do not expose privacy complaint or DSAR records to ordinary business members.
- Do not promise customer-hosted production before technical acceptance.
