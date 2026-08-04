# Firestore Security Review

## Scope
Review authentication, tenant isolation, privileged writes, audit integrity, validation, query behaviour and test coverage for all Firestore collections.

## Critical Finding
`assetChangeLogs` or equivalent trusted audit records must not inherit general client write permissions. Clients must be unable to forge, amend or delete audit evidence. Route trusted writes through a callable/server function that stamps actor UID, server time, tenant, project, action and request ID.

## Required Controls
- Deny all unauthenticated reads and writes unless intentionally public.
- Verify organisation and project membership from trusted records or claims.
- Check resource tenant IDs against the authenticated user's authorised tenant.
- Prevent clients changing ownership, tenant, creator, server timestamp or security classification fields.
- Separate admin-only operations from ordinary asset editing.
- Validate allowed keys, types, ranges and state transitions.
- Apply explicit rules to every collection and subcollection; avoid broad recursive permissions.
- Ensure list/query rules cannot expose cross-tenant records.
- Restrict bulk exports and destructive operations to approved roles.

## Audit and Activity Events
Opening an asset should not produce two permanent uncapped writes. Use one event definition, deduplicate by session/resource, sample or aggregate where appropriate, and document the lawful purpose and retention period.

## Test Matrix
Automated emulator tests must cover unauthenticated users, disabled users, each role, same-tenant access, cross-tenant denial, project boundaries, immutable fields, forged audit entries, deletion attempts, invalid payloads and privilege escalation.

## Deployment Gate
Rules must be version-controlled, peer-reviewed and tested in CI. Production deployment is blocked by failing security tests or unreviewed broad permissions.

## Evidence
Retain rule versions, test output, review approvals, findings, remediation commits and dates of production deployment.
