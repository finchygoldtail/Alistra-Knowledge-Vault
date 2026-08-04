# Service Level Agreement (SLA)

> **Draft for solicitor review.** This SLA must be completed with realistic targets supported by the chosen hosting architecture and support staffing.

## 1. Service covered

This SLA covers the production AlistraGIS services listed in the applicable Order Form. Development, test, preview, customer-managed infrastructure and unsupported third-party integrations are excluded unless expressly included.

## 2. Support hours

- Standard support: [09:00–17:00 UK time, Monday–Friday, excluding public holidays]
- Emergency security contact: [EMAIL/PHONE]
- Optional enhanced support: [DETAILS]

## 3. Incident priorities

| Priority | Definition | Initial response target | Update target |
|---|---|---:|---:|
| P1 Critical | Production unavailable for most users, confirmed serious security incident, or critical data-integrity risk with no workaround | [1 hour] | [Every 2 hours] |
| P2 High | Major function unavailable or materially degraded for many users | [4 business hours] | [Daily] |
| P3 Medium | Limited function affected; workaround exists | [1 business day] | [Every 3 business days] |
| P4 Low | Minor defect, question or enhancement request | [3 business days] | As agreed |

Response targets are acknowledgement and triage targets, not guaranteed resolution times.

## 4. Availability target

Target monthly availability: **[99.5%]** for the Supplier-hosted production service.

Availability percentage = (total measurement minutes − unavailable minutes) ÷ total measurement minutes × 100.

Excluded from unavailable minutes:

- planned maintenance notified at least [48 hours] in advance;
- emergency security maintenance;
- Customer systems, devices, internet connections or configuration;
- customer-hosted infrastructure;
- third-party failures outside the Supplier's reasonable control;
- suspension permitted by contract;
- force-majeure events;
- preview, beta and non-production services.

## 5. Planned maintenance

Normal maintenance window: [DAY/TIME]. The Supplier will seek to minimise disruption and provide reasonable notice. Urgent security fixes may be applied without the normal notice period.

## 6. Service credits

Service credits apply only where stated in the Order Form, are calculated against the affected monthly subscription fee, and are the Customer's financial remedy for availability failure except where law prevents this.

| Monthly availability | Proposed credit |
|---|---:|
| Below target but at least 99.0% | [5%] |
| Below 99.0% but at least 98.0% | [10%] |
| Below 98.0% | [20%] |

Claims must be submitted within [20] business days with supporting details. Total credits are capped at [20%] of the affected monthly fee.

## 7. Backup and recovery

For Supplier-hosted services:

- backup frequency: [daily plus platform-native replication];
- target recovery point objective (RPO): [24 hours];
- target recovery time objective (RTO): [8/24 hours depending on severity];
- restoration testing: [at least annually];
- retention: as set out in the backup and retention policies.

RPO and RTO are targets, not guarantees, unless expressly agreed otherwise. Customer-hosted backup responsibility rests with the Customer unless contracted separately.

## 8. Customer obligations

The Customer must provide sufficient incident detail, affected users, timestamps, screenshots, reproducible steps and authorised contacts. The Customer must not classify routine questions as P1 or P2.

## 9. Escalation

1. Support desk: [CONTACT]
2. Technical lead: [CONTACT]
3. Commercial escalation: [CONTACT]
4. Security/data protection: [CONTACT]

## 10. Problem management

For qualifying P1 incidents, the Supplier will provide a written summary or root-cause analysis within [10] business days where reasonably possible, including corrective actions without exposing sensitive security information.

## 11. Changes to this SLA

Material changes require written agreement or apply from renewal after reasonable advance notice. Security and operational procedures may be updated where they do not materially reduce the contracted service.
