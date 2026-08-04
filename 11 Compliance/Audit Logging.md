# Audit Logging

## Purpose
Create reliable evidence of security-sensitive and business-critical activity without excessive or unnecessary monitoring.

## Events to Record
Authentication changes, failed privileged access, role and membership changes, asset creation/update/deletion, approvals, exports, configuration changes, support actions, security-rule changes, incident actions and break-glass access.

## Required Fields
Event ID, server timestamp, actor UID/service identity, organisation, project, action, target type/ID, outcome, request/correlation ID and approved reason where relevant. Avoid storing unnecessary payloads, secrets or full personal-data records.

## Integrity
Trusted audit events must be created server-side. Ordinary clients cannot create, edit or delete them. Administrative access to logs is read-only by default and tightly restricted.

## Viewed Events
Do not write duplicate permanent events whenever an asset is opened. Use one implementation with deduplication, aggregation or sampling, a documented purpose and a proportionate retention period.

## Monitoring
Alert on repeated authentication failures, denied cross-tenant access, privilege changes, mass exports/deletions, disabled-user activity and unusual support-agent actions.

## Retention
Set retention by event category and legal/business need. Security logs should generally be kept long enough to investigate delayed incidents, while routine usage analytics should be shorter and aggregated where possible.

## Review
Review log completeness, alert effectiveness, access rights and retention quarterly and after incidents.
