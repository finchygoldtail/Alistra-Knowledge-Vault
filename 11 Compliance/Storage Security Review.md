# Storage Security Review

## Scope
Firebase Storage and any future AWS, Azure or customer-hosted file service used for photos, evidence, documents, exports and backups.

## Required Controls
- Authenticate every non-public request.
- Use organisation/project/resource-scoped paths and verify membership independently of filenames.
- Prevent users choosing another tenant's path or replacing ownership metadata.
- Allow only approved file types and realistic size limits.
- Validate actual file signatures server-side for high-risk uploads; do not trust extension or browser content type alone.
- Block executable, script and archive formats unless explicitly required and safely processed.
- Scan externally supplied files for malware where the risk warrants it.
- Generate downloads through authorised application flows; use short-lived signed URLs where applicable.
- Disable public buckets and accidental directory listing.
- Encrypt in transit and at rest; document any customer-managed-key requirements.
- Apply lifecycle and deletion rules that match the retention schedule.

## Evidence Photos
Evidence must retain tenant, project, asset, uploader, capture/upload time and integrity metadata. Editing or replacement should create a new version or auditable event rather than silently overwriting evidence.

## Exports and Backups
Exports and backups are sensitive copies. Restrict creation and download, expire temporary exports, log large exports and protect backup credentials separately from production credentials.

## Testing
Test unauthenticated denial, cross-tenant reads/writes, path traversal attempts, oversized files, disallowed formats, metadata spoofing, deleted-user access and expired links.

## Review Outcome
Record each finding with severity, affected rule/path, evidence, owner, target date and remediation verification.
