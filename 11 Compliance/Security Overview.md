# Security Overview

## Security Model
AlistraGIS uses defence in depth across identity, API access, application authorisation, Firestore, file storage, audit records, deployment and operational procedures.

## Core Principles
- Deny by default and grant least privilege.
- Enforce permissions on trusted server and database boundaries, never only in the interface.
- Isolate every organisation, project and area using verified membership claims and resource ownership.
- Keep production, test and demonstration data separate.
- Record security-sensitive actions in tamper-resistant logs.
- Protect secrets outside source control and rotate them after exposure or personnel changes.

## Architecture Controls
1. **Identity:** Firebase Authentication with approved sign-in methods, verified accounts and MFA for privileged users.
2. **Authorisation:** central role and permission service; server-side checks for every privileged operation.
3. **API:** authenticated gateway, schema validation, rate limits, request IDs and consistent error handling.
4. **Firestore:** tenant-scoped rules, immutable trusted fields, explicit collection rules and automated emulator tests.
5. **Storage:** organisation/project paths, ownership checks, file-size and content-type restrictions, malware scanning where appropriate.
6. **Hosting:** protected deployment environments, preview/production separation, dependency scanning and rollback capability.
7. **Monitoring:** alerting for authentication abuse, permission failures, unusual exports, destructive actions and cost spikes.

## Data Protection
Use encryption in transit and provider-managed encryption at rest. Highly sensitive customer requirements may require customer-managed keys, dedicated projects or customer-hosted storage. Data exports and backups must receive the same protection as live data.

## Secure Development Lifecycle
Every material change requires threat consideration, peer review, automated tests and release evidence. Security findings are classified Critical, High, Medium or Low and tracked to closure with an owner and deadline.

## Immediate Risks
- Duplicate uncontrolled viewed-event writes may increase cost and create excessive personal activity records.
- Client-accessible audit/change-log collections can undermine evidential integrity.
- Multi-tenant rules require systematic negative testing to prove one customer cannot access another customer's data.
- Password, access, upgrade and incident requests need a controlled support-desk process.

## Review
Review this overview after architecture changes, new data integrations, new authentication methods, major releases or security incidents.
