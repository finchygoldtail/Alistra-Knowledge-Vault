---
title: AlistraGIS Client Framework Agreement
status: draft-for-solicitor-review
updated: 2026-09-08
owner: Alistair
related: ["[[14 Client Order Form and Service Schedule]]", "[[15 Hosting and Data Responsibility Schedule]]", "[[02 Software and SaaS Licence Agreement]]", "[[03 Service Level Agreement]]", "[[DPA Requirements]]", "[[Client Pricing Pack]]"]
---

# AlistraGIS Client Framework Agreement

> **Draft for UK technology/SaaS solicitor review before signature.** This framework is designed so the commercial deal can vary by modules, user count, projects, hosting model, support level and implementation requirements without rewriting the full contract for each client.

## 1. Parties

This Framework Agreement is between:

**Supplier:** Alistra GIS Ltd, trading as AlistraGIS, company number 17361925, registered in England and Wales, of [REGISTERED OFFICE ADDRESS] (**Supplier**); and

**Customer:** the legal entity identified in the applicable Order Form (**Customer**).

The Supplier and Customer are each a **Party** and together the **Parties**.

## 2. Contract structure

This Framework Agreement governs all Orders entered into under it. Each signed Order Form creates a binding Order for the services described in that Order Form.

The contract for an Order consists of, in descending order of precedence unless the Order Form expressly states otherwise:

1. the signed [[14 Client Order Form and Service Schedule]];
2. any expressly agreed Special Conditions;
3. any signed Data Processing Agreement;
4. the [[15 Hosting and Data Responsibility Schedule]];
5. the [[03 Service Level Agreement]];
6. the [[02 Software and SaaS Licence Agreement]];
7. the [[01 Standard Terms and Conditions]];
8. this Framework Agreement; and
9. any incorporated policies referenced by the Order.

If there is a conflict, the higher document in the list prevails only to the extent of that conflict.

## 3. Modular service model

AlistraGIS is licensed on a modular basis. The Customer receives access only to the modules, environments, APIs and capabilities listed in the Order Form.

The current licence engine can control, among other things:

- platform plan type;
- authorised user/seat limit;
- project limit;
- enabled feature modules;
- licence status and term.

No module is included merely because it exists elsewhere in the AlistraGIS platform, documentation, roadmap, demonstration environment or marketing material.

Additional modules may be added during the term through a signed Change Order or updated Order Form. Removal of modules may take effect only at the agreed renewal/change date unless the Parties agree otherwise.

## 4. Authorised users and seats

The Order Form states the purchased seat allowance.

Each active Customer user counts as a licensed seat except Supplier platform/support accounts expressly excluded by the licence model. Customer accounts may not be shared between individuals.

The Customer is responsible for promptly disabling users who no longer require access and for maintaining accurate roles and permissions.

Where the Customer exceeds its purchased seat allowance, the Supplier may:

- prevent creation/activation of additional users;
- offer an upgrade or additional seat pack; and/or
- charge agreed overage/additional-seat fees where the Order Form permits.

## 5. Projects and environments

The Order Form may limit active projects, geographic areas, environments or other measurable usage. Additional project capacity may be purchased by Change Order.

Test, training, demonstration and production environments must not be assumed to have identical data, availability, backup or support commitments unless expressly stated.

## 6. Hosting options

The Order Form must select one approved hosting model.

### 6.1 AlistraGIS-managed shared hosting

The Supplier operates the application using Supplier-selected cloud infrastructure and approved subprocessors. Unless otherwise agreed, this is the standard production model.

### 6.2 AlistraGIS-managed dedicated hosting

Where offered, the Supplier provides a logically or physically dedicated customer environment or dedicated data layer. Exact isolation, region, backup, recovery and service boundaries must be stated in the Order Form.

### 6.3 Customer-selected / customer-hosted infrastructure

Where the Customer requires its own Azure, AWS, PostgreSQL/PostGIS or other approved server/cloud environment, activation is subject to technical readiness and a supported architecture confirmed by the Supplier.

The Customer is responsible for the Customer-controlled cloud account, infrastructure charges and responsibilities allocated to it in the Hosting Schedule. The Supplier is not obliged to support an arbitrary provider, version or architecture that has not been approved in writing.

### 6.4 Current implementation caveat

As at 8 September 2026, AlistraGIS-managed Firebase/GCP hosting is the production-supported model. Customer-hosted Azure/AWS/PostGIS architecture is built toward but remains subject to customer-specific provisioning, technical validation and removal of the existing fail-closed production guard for that customer. It must not be sold as an instant configuration change until those checks are complete.

## 7. Data ownership and data roles

The Customer retains ownership of Customer Data.

For customer-controlled project, workforce, evidence and operational personal data, the intended model is normally Customer as controller and Supplier as processor. The Supplier may separately act as controller for its own account administration, security, billing/licensing, support, supplier and business-management information.

The final allocation and processor terms are governed by the signed Data Processing Agreement and must be consistent with the actual hosting/configuration selected in the Order Form.

The Customer warrants that it has the rights and lawful basis necessary to provide Customer Data to the service.

## 8. Data location, subprocessors and international transfers

The Hosting Schedule and DPA must identify the relevant hosting model and approved subprocessors.

Where processing or storage occurs outside the UK or another agreed region, the Parties will rely on the appropriate lawful transfer mechanism where required.

The Supplier must not make an absolute UK-only or EU-only data-residency commitment unless the selected configuration has been technically verified to support it.

## 9. Implementation and onboarding

Implementation may include:

- tenant/company configuration;
- module and licence setup;
- user import;
- project/data import;
- branding;
- permissions workshops;
- training;
- integration/API setup;
- hosting/environment provisioning;
- migration or transformation services.

Only the implementation items listed in the Order Form are included in the agreed price. Material additional work requires a Change Order or is charged at the agreed professional-services rate.

## 10. Support and service levels

The Customer receives the support level listed in the Order Form. The SLA defines response targets, service hours, planned maintenance and exclusions.

Response times are not guaranteed resolution times unless expressly stated.

Customer-hosted incidents may be excluded from Supplier availability commitments where the root cause lies within Customer-controlled infrastructure, network, credentials, third-party services or configuration.

## 11. Security

The Supplier is responsible for reasonable security controls over Supplier-managed application components. The Customer is responsible for its users, devices, role assignments, source data, customer-controlled credentials and customer-hosted infrastructure.

Each Party must notify the other without undue delay of a suspected security event materially affecting the other Party's data or contracted service.

Personal-data incidents are additionally governed by the DPA and [[Data Breach and Incident Response]].

## 12. Data protection complaints and individual rights

The Supplier maintains a [[12 Data Protection Complaints Procedure]] and [[Data Subject Rights Procedure]].

Where the Customer is controller, the Customer remains responsible for controller decisions and the Supplier will provide reasonable processor assistance as defined in the DPA.

The Parties must maintain operational contact routes so that complaints, rights requests and breach notices are not delayed by uncertainty over ownership.

## 13. Fees and invoicing

Fees are set out in the Order Form and may comprise:

- base platform licence;
- module fees;
- additional user/seat fees;
- project capacity;
- hosting/environment fees;
- storage/usage overages;
- support tier;
- onboarding/implementation;
- training;
- migration;
- professional services;
- API/AI/third-party usage;
- bespoke development.

Unless stated otherwise, prices are exclusive of VAT and third-party/customer infrastructure charges.

No price in the [[Client Pricing Pack]] becomes contractually binding until included in a signed Order Form or quotation accepted under this Framework Agreement.

## 14. Annual review and changes

The Order Form must state the subscription term, renewal mechanism and any pricing review provision.

The Supplier may change standard list prices for future Orders or renewals on the notice period stated in the Order Form. Existing fixed-term pricing remains unchanged during that fixed term unless the Customer increases scope or usage, or a contractually permitted pass-through cost applies.

## 15. Change control

A Change Order should be used where the Customer requests a material change to:

- modules;
- user count;
- project count;
- hosting model;
- region;
- integrations;
- support tier;
- data migration;
- bespoke functionality;
- implementation scope; or
- price.

A Change Order must describe the change, dependencies, price impact, effective date and any effect on security, DPA, SLA or delivery dates.

## 16. Customer responsibilities

The Customer must:

- use the service lawfully and only for its authorised business purposes;
- control and review its users and roles;
- supply accurate and lawful source data;
- obtain necessary notices, permissions and lawful bases for Customer Data;
- verify infrastructure/network information before safety-critical or physical works;
- maintain Customer-controlled infrastructure where applicable;
- follow security guidance and report suspected compromise;
- pay agreed fees when due.

AlistraGIS is an information, workflow, GIS and operational-management system. It does not replace statutory searches, safe-working procedures, engineering verification, surveys, permits, professional judgement or other checks required before physical works.

## 17. Intellectual property

The Supplier retains all rights in AlistraGIS, including source code, APIs, schemas, workflows, interfaces, templates, documentation, methods and improvements except where a separate signed agreement expressly assigns identified rights.

The Customer retains rights in Customer Data and Customer-owned materials.

Bespoke development remains Supplier IP unless the Order Form expressly states otherwise.

## 18. Confidentiality

Each Party must protect the other's Confidential Information and use it only to perform or receive the contracted services, subject to customary exceptions for public, independently developed, lawfully received or legally compelled information.

A separate NDA may be used before the Framework Agreement is signed.

## 19. Warranties and third-party dependencies

The Supplier will provide the contracted service with reasonable skill and care.

The Customer acknowledges that cloud, mapping, internet, telecommunications, AI and other third-party services may affect availability or functionality. Third-party terms may apply.

No warranty is given that Customer Data, imported infrastructure records, map data, AI-assisted output or third-party source information is complete or suitable for safety-critical reliance without independent verification.

## 20. Liability

**Solicitor completion required before signature.**

The final agreement must state:

- overall liability cap(s);
- treatment of data-protection/security liability;
- IP infringement allocation;
- excluded indirect/consequential losses;
- treatment of loss of profit/revenue/data;
- any higher or separate cap for confidentiality/data incidents;
- non-excludable liabilities;
- customer indemnities, if appropriate;
- infrastructure/safety reliance exclusions; and
- insurance alignment.

No placeholder liability cap should be converted into a contractual promise without solicitor and insurance review.

## 21. Term, renewal and termination

Each Order starts and ends as stated in its Order Form.

Termination rights for material breach, insolvency, prolonged suspension and non-payment are governed by the Standard Terms/SaaS Licence and any Order-specific terms.

Termination of one Order does not automatically terminate other Orders unless stated.

## 22. Exit, export and deletion

Before termination, the Customer should use available export functionality or purchase agreed migration assistance.

The Order Form must state the normal exit window, and the DPA/retention schedule governs deletion, backup expiry and lawful retention exceptions.

Customer-hosted environments may require the Customer to perform infrastructure-side deletion, credential revocation or storage disposal.

## 23. Assignment, subcontracting and change of control

Assignment and subcontracting restrictions are governed by the Standard Terms. Approved subprocessors may be used in accordance with the DPA.

## 24. Notices

Contract and legal-notice addresses must be stated in the Order Form. Data-protection, security and support routes may be different operational addresses.

## 25. Governing law and dispute resolution

**Solicitor completion required.** The intended starting position is the law of England and Wales and courts of England and Wales for B2B customers, subject to final review and any negotiated dispute/escalation process.

## 26. Entire agreement

The documents listed in section 2 constitute the agreement for each Order and replace prior discussions concerning that Order, except for fraud or any matter that cannot lawfully be excluded.

## 27. Signatures

This Framework Agreement may be signed electronically and in counterparts.

**For Alistra GIS Ltd**  
Name: ______________________________  
Title: _______________________________  
Signature: ___________________________  
Date: _______________________________

**For the Customer**  
Legal name: __________________________  
Name: ______________________________  
Title: _______________________________  
Signature: ___________________________  
Date: _______________________________
