# Incident Response Plan

## Objective
Contain, investigate and recover from security, privacy and availability incidents while preserving evidence and meeting contractual and legal obligations.

## Severity
- **Critical:** confirmed large-scale breach, destructive compromise, widespread outage or loss of control.
- **High:** suspected unauthorised access, major customer impact or serious control failure.
- **Medium:** limited incident with contained impact.
- **Low:** minor event or policy breach without material impact.

## Response Process
1. **Detect and report:** open a security ticket and record time, reporter, symptoms and affected systems.
2. **Triage:** assign incident lead, severity, scope and immediate safety actions.
3. **Contain:** revoke sessions/keys, disable affected functions, isolate tenants or roll back releases without destroying evidence.
4. **Investigate:** preserve logs, establish timeline, identify affected data and root cause.
5. **Notify:** involve leadership, customers, insurers, legal advisers and regulators as required. UK personal-data breaches requiring ICO notification must be assessed promptly against the applicable 72-hour requirement.
6. **Recover:** restore safe service, monitor closely and validate data integrity.
7. **Review:** document lessons, corrective actions, owners and deadlines.

## Evidence Handling
Use server timestamps, request IDs and read-only copies. Restrict evidence access and record who collected or reviewed it.

## Communications
Only authorised people communicate externally. Messages must be accurate, dated, clear about known/unknown facts and avoid speculation.

## Testing
Run at least annual tabletop exercises and additional exercises after major architecture changes. Include tenant breach, compromised admin, destructive deletion, supplier outage and lost device scenarios.
