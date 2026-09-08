---
title: Data Protection Complaints Procedure
status: operational-draft-for-professional-review
updated: 2026-09-08
owner: Alistair
related: ["[[03 GDPR Data Register]]", "[[Data Subject Rights Procedure]]", "[[Data Breach and Incident Response]]", "[[08 Privacy Notice and Website Legal Notices]]", "[[DPA Requirements]]"]
---

# Data Protection Complaints Procedure

> **Status:** Operational draft for AlistraGIS. The statutory complaints duty is now in force in the UK. Contract wording and any customer-specific allocation should still be checked by the solicitor/privacy adviser before commercial launch.

## 1. Purpose

Alistra GIS Ltd must provide people with a clear route to complain about how personal data is handled. This procedure applies to complaints concerning AlistraGIS's own controller processing and to complaints received by AlistraGIS about customer-controlled personal data where AlistraGIS acts as processor.

This procedure is separate from, but may overlap with, a subject access request, correction request, erasure request, objection, restriction request or personal-data-breach report.

## 2. Current legal baseline

The Data (Use and Access) Act 2025 complaints provisions are in force. The operational baseline used by AlistraGIS is:

- provide a clear way for a person to raise a data-protection complaint;
- acknowledge the complaint within **30 days of receipt**;
- without undue delay, take appropriate steps to investigate the complaint;
- keep the complainant appropriately informed during the investigation; and
- tell the complainant the outcome without undue delay.

**Authority checked 8 September 2026:** ICO guidance and the ICO's 23 June 2026 notice confirming the complaints duty is in force.

## 3. Complaint channels

A complaint may be received through any reasonable route, including:

- privacy/data-protection email;
- the AlistraGIS support system;
- direct written correspondence;
- an authorised customer administrator;
- a future website or in-app privacy complaint form.

**Current privacy contact:** Alistair.Grantham@alistragis.com

A complaint does not have to contain the words "data protection complaint" to count. If the substance is dissatisfaction about collection, use, sharing, accuracy, access, retention, deletion, security or other handling of personal data, it must be assessed under this procedure.

## 4. Complaint register

Every complaint must be recorded with, where applicable:

- complaint reference;
- date/time received;
- date acknowledged;
- complainant name and contact details;
- data subject, if different;
- customer/business/tenant involved;
- summary of the issue;
- whether AlistraGIS is controller, processor or the role is still being assessed;
- related DSAR, support ticket or incident reference;
- identity/authority checks where disclosure or rights handling is involved;
- investigator/owner;
- actions taken and evidence reviewed;
- updates sent to the complainant;
- outcome and reasons;
- remediation/corrective action;
- closure date;
- escalation to customer/controller, solicitor, insurer or ICO where applicable.

Retention of the complaint record must follow the approved [[Data Retention Schedule]] rather than an invented period in this procedure.

## 5. Triage on receipt

On receipt, determine whether the matter is primarily:

1. a data-protection complaint;
2. a data-subject-rights request;
3. a suspected personal data breach/security incident;
4. a customer support/service complaint with a data-protection element; or
5. more than one of the above.

Where more than one process applies, link the records and run the necessary procedures in parallel. Do not treat a complaint as resolved merely because a DSAR response has been supplied.

## 6. Controller / processor routing

### AlistraGIS controller data

Where AlistraGIS determines the purpose and means of processing, for example its own account administration, support, security, billing/licensing, supplier or business-contact records, AlistraGIS investigates and responds directly.

### Customer-controlled data

Where the customer is controller and AlistraGIS is processor for project, workforce, evidence or other customer-controlled data:

- promptly identify the relevant customer/controller;
- notify or route the matter to the authorised customer contact where appropriate;
- preserve relevant evidence;
- assist the customer according to the DPA and documented instructions;
- do not independently make a legal decision reserved to the controller unless AlistraGIS has a separate controller role for part of the processing.

If role allocation is unclear, escalate rather than guessing.

## 7. Acknowledgement

The complaint must be acknowledged within 30 days of receipt. Good operational practice is to acknowledge substantially sooner where possible.

The acknowledgement should include:

- the complaint reference;
- a short summary of what AlistraGIS understands the complaint to be;
- the contact route for updates;
- any information reasonably needed to investigate;
- whether another controller/customer is involved, where appropriate; and
- a statement that the complaint will be investigated and the outcome communicated without undue delay.

## 8. Investigation

The investigator should take proportionate steps which may include:

- reviewing account/profile records;
- reviewing relevant Firestore/Storage records;
- reviewing tickets, asset-change logs and audit events;
- checking permissions and tenant access;
- reviewing uploaded evidence/photos;
- checking processor/subprocessor involvement;
- checking relevant contracts, privacy notices, DPA and retention rules;
- interviewing relevant staff or customer administrators;
- confirming whether a security incident occurred;
- checking whether information is inaccurate, excessive, retained too long or disclosed incorrectly.

Investigation access must follow least privilege. Do not create new unnecessary copies of personal data merely to investigate a complaint.

## 9. Keeping the complainant informed

Where the complaint cannot be concluded promptly, provide reasonable progress updates. Do not give speculative conclusions while investigation is still underway.

## 10. Outcome response

The outcome should state, in clear language:

- what was investigated;
- the conclusion reached;
- material reasons for the conclusion;
- any correction, deletion, access change or other remediation completed or planned;
- anything AlistraGIS cannot do and why;
- where a customer/controller must take the decision instead;
- the route for further questions; and
- the person's right to raise concerns with the Information Commissioner's Office where applicable.

## 11. Corrective action

A complaint must be used to identify systemic issues where relevant. Corrective action may include:

- changing permissions or security rules;
- correcting inaccurate data;
- deleting/minimising data where lawful;
- changing retention configuration;
- updating privacy information or customer guidance;
- retraining staff;
- changing a subprocessor/configuration;
- creating an engineering/security task;
- updating the DPIA or data register;
- triggering the incident-response process.

## 12. No retaliation / service impact

A person must not be penalised merely for making a genuine data-protection complaint. Any account suspension or restriction must have an independent contractual/security basis and be recorded separately.

## 13. Operational actions before first paying customer

- [ ] Create a dedicated support category: **Privacy / Data Protection Complaint**.
- [ ] Add complaint reference, received date, acknowledgement date, owner and status fields.
- [ ] Add an admin-only complaint register/report.
- [ ] Add a public/in-app route explaining how to complain.
- [ ] Update the Privacy Notice complaints section to describe this process.
- [ ] Nominate primary privacy lead and deputy.
- [ ] Test one mock complaint end-to-end.
- [ ] Confirm the customer-controller handoff wording in the DPA/framework agreement.

## 14. Professional review points

Ask the solicitor/privacy adviser to confirm:

- controller/processor complaint handling split;
- any additional statutory wording required in customer-facing notices;
- escalation/record-retention approach;
- interaction with DSAR and breach procedures; and
- whether the framework agreement/DPA should impose shorter contractual response times between Customer and Supplier.
