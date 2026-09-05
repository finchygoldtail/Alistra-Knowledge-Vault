# Developer Access Control Register

## Policy

Developer access must follow least privilege, named individual accounts, multi-factor authentication and prompt removal when access is no longer required. Shared accounts are prohibited except for documented emergency accounts held securely.

## Systems in scope

- GitHub repositories and organisations
- Vercel projects and teams
- Firebase / Google Cloud projects
- Domain registrar and DNS
- Mapping and third-party API providers
- Production databases and storage
- Monitoring, support and CI/CD systems

## Access register

| Person | Employer / role | System | Permission | Business reason | Approved by | Granted | Review date | Removed |
|---|---|---|---|---|---|---|---|---|
| [complete] | [complete] | [complete] | [read/write/admin] | [complete] | [complete] | [date] | [date] | [date] |

## Minimum controls

- [ ] MFA enabled for every privileged account.
- [ ] Unique named accounts used.
- [ ] Repository access limited to required repositories.
- [ ] Production write access restricted and separately approved.
- [ ] Branch protection and pull-request review enabled for critical branches.
- [ ] Secrets stored in managed environment variables or secret managers, never source control.
- [ ] Access reviewed at least quarterly.
- [ ] Leavers and contractors removed immediately at end of engagement.
- [ ] Material access changes logged.
- [ ] Recovery codes and emergency accounts securely controlled.

## Joiner, mover and leaver process

### Joiner

1. Confirm signed confidentiality and IP terms.
2. Approve the minimum permissions required.
3. Require MFA before granting access.
4. Record access in this register.

### Mover

1. Review permissions when responsibilities change.
2. Remove obsolete access before adding new access.
3. Record approver and date.

### Leaver

1. Disable or remove all access immediately.
2. Rotate shared secrets the person could access.
3. Recover company devices and files.
4. Confirm no local copies of confidential code or data are retained.
5. Record completion and evidence.

## Access review record

| Review date | Reviewer | Systems checked | Issues found | Corrective action | Completed |
|---|---|---|---|---|---|
| [date] | [name] | [systems] | [details] | [action] | [date] |
