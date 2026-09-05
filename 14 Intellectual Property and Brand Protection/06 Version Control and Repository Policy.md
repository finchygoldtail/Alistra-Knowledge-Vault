# Version Control and Repository Policy

## Standard

GitHub is the approved version-control platform for AlistraGIS unless a customer contract requires another controlled platform. All production source code, infrastructure configuration, database rules, deployment configuration and material technical documentation must be version-controlled.

## Repository controls

- Repositories containing proprietary AlistraGIS code should be private unless publication is deliberately approved.
- The default production branch must be protected.
- Material changes should be made through pull requests and reviewed before merge.
- Direct pushes to production branches should be restricted.
- Force-push and branch deletion should be disabled for protected branches.
- CI checks should run before merge where available.
- Releases should be tagged and linked to deployment records.
- Repository administrators should be limited and reviewed quarterly.

## Commit and review requirements

Each material change should include:

- A clear commit message.
- A linked issue, ticket or change reason where practical.
- Testing evidence proportionate to risk.
- Security and data-migration notes where applicable.
- Reviewer approval for critical security, permissions, billing, data or deployment changes.

## Secrets and sensitive information

Never commit passwords, API keys, service-account files, production exports, customer data, personal data or confidential customer documents. Suspected secret exposure must trigger immediate revocation, rotation and incident review; deleting the file from the latest commit alone is insufficient.

## Backup and continuity

- Maintain recoverable copies or mirrors for business-critical repositories.
- Ensure more than one authorised person or controlled business account can recover access.
- Record ownership of organisations, billing, domains and deployment integrations.
- Test restoration or repository transfer periodically.

## Third-party and generated code

Third-party code must be licence-reviewed. AI-generated or externally supplied code must undergo the same review, testing, security and ownership checks as human-written code.

## Current implementation record

| Control | Status | Evidence / action |
|---|---|---|
| GitHub implemented | Complete | Repositories are managed through GitHub |
| Production branch protection | [confirm] | [link or action] |
| MFA for administrators | [confirm] | [evidence] |
| Pull-request reviews | [confirm] | [policy/ruleset] |
| Secret scanning | [confirm] | [setting/evidence] |
| Dependency alerts | [confirm] | [setting/evidence] |
| Repository backup | [confirm] | [method] |
| Quarterly access review | [confirm] | [[04 Developer Access Control Register]] |
