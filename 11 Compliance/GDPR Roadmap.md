# GDPR Roadmap

## Objective
Prepare AlistraGIS to demonstrate practical UK GDPR and Data Protection Act 2018 compliance. This roadmap is an engineering and operational plan, not legal advice.

## Phase 1 — Discover and Stabilise
- Create a full personal-data inventory covering Auth, Firestore, Storage, logs, support tickets, analytics, backups and third-party services.
- Record data subjects, data fields, purposes, lawful bases, locations, recipients and retention periods.
- Identify special-category, criminal-offence, employee and child data and prohibit collection unless specifically approved.
- Fix critical security findings, particularly forgeable/deletable audit records and uncontrolled high-volume viewed-event logging.
- Confirm controller, processor and subprocessor responsibilities for each deployment model.

## Phase 2 — Governance
- Create Records of Processing Activities.
- Define privacy ownership, engineering ownership and incident responsibilities.
- Establish DPIA triggers for mapping, workforce monitoring, location data, AI features and large-scale customer deployments.
- Execute processor agreements and International Data Transfer safeguards where required.
- Establish annual supplier and subprocessor review.

## Phase 3 — Data Subject Rights
Implement verified workflows for access, correction, deletion, restriction, objection, portability and consent withdrawal. Requests must be logged, identity checked, assigned, completed within the applicable deadline and supported by evidence.

## Phase 4 — Privacy by Design
- Collect only necessary data.
- Default new fields to private and tenant-scoped.
- Separate customer production data from development and demonstrations.
- Use pseudonymous identifiers where practical.
- Require retention classification for every new collection and file category.
- Add privacy and security acceptance criteria to product tickets.

## Phase 5 — Retention and Deletion
Implement automated lifecycle rules where safe, legal holds, account closure procedures, backup expiry and auditable deletion reports. Customer contracts must state who authorises deletion and what happens at termination.

## Phase 6 — Assurance
- Run Firestore and Storage rule tests in CI.
- Perform vulnerability assessment and independent penetration testing before enterprise launch.
- Complete restore, breach and data-subject-request exercises.
- Assemble an evidence pack containing policies, diagrams, test results, access reviews, training records and supplier documentation.

## Release Gates
Production onboarding is blocked when critical tenant-isolation, authentication, authorisation, backup or breach-response controls are untested. High-risk processing is blocked until its DPIA and approvals are complete.

## Success Measures
No open critical security findings; documented processing inventory; tested rights workflow; approved retention schedule; current contracts and subprocessors; successful restore test; completed incident exercise; and evidence available for customer due diligence.
