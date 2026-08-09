# FRIDAY AI — Parked Prototype

## Status

FRIDAY has been removed from the production AlistraGIS application and parked as a separate local prototype under:

`C:\Projects\fibre-gis\Friday AI`

It is not production-ready and must not be deployed, enabled for AlistraGIS users, or used commercially until provider licensing, commercial-use terms, operating cost, security, data handling and support requirements have been reviewed and approved.

## What was removed from AlistraGIS

- FRIDAY Health dashboard and Ask FRIDAY UI.
- Firebase `fridayChat` callable export.
- NVIDIA/OpenAI dependency from the production Functions package.
- FRIDAY audit event types and rate-limit Firestore rule/test fixture.
- FRIDAY health CI workflow and root scan scripts.
- FRIDAY marketing and public capability claims.

## What is preserved

The `Friday AI` folder preserves the deterministic scanner, rule packs, dashboard prototype, Ask FRIDAY NVIDIA prototype, tests and phase documentation for future development.

The parked backend prototype still expects AlistraGIS storage/auth adapters. It is intentionally not wired to a deployable project.

## Future integration gates

Before considering integration:

1. Confirm provider licensing and commercial-use permission.
2. Define a safe operating budget, quotas and rate limits.
3. Define company, project, area and polygon scoping.
4. Approve data minimisation, redaction, retention and tenant isolation.
5. Define production monitoring, failure handling and permissions.
6. Prepare a reviewed integration and rollback plan.

## Implementation handover

- Main application typecheck: passed.
- Frontend production build: passed.
- Firebase Functions build: passed.
- Storage tests: 245 passed.
- Component tests: 8 passed.
- Main source scan: no FRIDAY/NVIDIA references remain outside the parked project.
- Known unrelated issue: 15 existing lint errors remain in `src/components/JointMapManager.tsx`.
- Firestore emulator rule test was not run because the Firebase CLI is unavailable in the local environment.
- No commit, push or deployment was performed.
