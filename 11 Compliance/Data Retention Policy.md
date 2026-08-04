# Data Retention Policy

## Principle
Keep personal and customer data only for a defined purpose and no longer than necessary. Contractual, legal-hold and customer-hosting requirements may alter the schedule and must be documented.

## Baseline Schedule
| Data Category | Baseline | Disposal |
|---|---|---|
| Active customer operational data | Contract term | Return/export then verified deletion |
| Closed customer data | Up to 90 days unless agreed otherwise | Delete from live systems |
| Routine usage/view analytics | 30–90 days | Aggregate or delete |
| Security and privileged audit logs | 12–24 months | Secure deletion |
| Support tickets | 24 months after closure | Delete/anonymise |
| Failed login and abuse telemetry | 6–12 months | Delete |
| Temporary exports | 7–30 days | Automatic expiry |
| Backups | Defined rolling cycle, normally 30–90 days | Expire automatically |
| Finance and contract records | Applicable statutory period | Secure deletion |

## Requirements
Each collection, storage path and log stream must have an owner, purpose, retention period and deletion method. New data stores cannot launch without these fields.

## Deletion
Deletion must cover indexes, derived data, exports and scheduled backup expiry. Where immediate backup deletion is impractical, data remains protected, inaccessible in normal operation and expires under the documented cycle.

## Exceptions
Legal holds, disputes, fraud investigations and statutory duties may suspend deletion. Record the authority, scope, approver and review date.

## Customer Exit
Confirm export format, transfer method, termination date, deletion authorisation, backup expiry and completion evidence.

## Review
Review annually and whenever processing purposes, suppliers, contracts or law materially change.
