# Permission Matrix

## Roles
Roles must be centrally defined and enforced server-side. UI visibility is not a security control.

| Capability | User | Manager | Admin | Super Admin |
|---|---:|---:|---:|---:|
| View assigned projects and map assets | Yes | Yes | Yes | Yes |
| Create/update permitted operational records | Yes | Yes | Yes | Yes |
| Draw or modify map geometry | No | No | Yes | Yes |
| Use navigation, measure and layer controls | Yes | Yes | Yes | Yes |
| Approve audits/walk-offs | No | Yes | Yes | Yes |
| View commercial data | No | Approved only | Yes | Yes |
| Manage project membership | No | Limited | Yes | Yes |
| Create/disable users | No | No | Yes | Yes |
| Change roles | No | No | Limited | Yes |
| Export customer data | No | Approved only | Yes | Yes |
| View security/audit logs | No | Limited | Yes | Yes |
| Delete protected evidence or logs | No | No | No | Controlled break-glass only |
| Configure integrations/secrets | No | No | Limited | Yes |

## Rules
- Access is scoped by organisation, project and where necessary area.
- A role never grants access to another customer's data.
- Privileged access requires MFA and should use named accounts.
- Temporary elevation must have an approver, reason and expiry.
- Departing or suspended users are disabled promptly and active sessions revoked.
- Service accounts receive only the permissions required for their function.

## Access Reviews
Review privileged users monthly and all users quarterly. Record reviewer, date, exceptions, removals and approvals.

## Change Control
Permission changes must originate from an authorised support or administration request, be logged with before/after values and be independently reviewable.
