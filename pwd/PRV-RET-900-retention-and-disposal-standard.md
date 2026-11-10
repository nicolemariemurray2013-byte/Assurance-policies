# Information Retention and Secure Disposal Standard (multi-account test)

Document id: PRV-RET-900. Version 1.0. Effective 2026-09-01. Next review 2026-12-31.
Owner: Privacy Engineering. Approved by: Chief Privacy Officer, 2026-09-01.

## 1. Purpose
This standard governs how long personal information is retained across every AWS account in
the organization, and how it is protected from erasure or destruction while retained.

## 2. Retention periods by information class
| Class | Retention | Stated purpose |
|---|---|---|
| Customer contact records | 24 months after last interaction | Service delivery and support history |
| Access and audit logs | 400 days | Security investigation and regulatory audit |
| Operational telemetry | 30 days | Capacity and reliability engineering |
| Financial transaction records | 7 years | Statutory tax and accounting obligation |

Personal information is retained only for the period stated above and only for the stated
purpose. Retention beyond the stated period is permitted only where a specific law requires it,
and each such extension is recorded in the retention register with its legal basis.

## 3. Protection from erasure or destruction during the retention period
While information is within its retention period it is protected against premature erasure and
against destruction by the following controls, applied in every account:
1. Object versioning is enabled on every bucket holding personal information, so an overwrite or
   delete creates a recoverable prior version rather than destroying data.
2. Lifecycle rules express the retention period; expiration is configured only at the end of it.
3. Delete permissions on retention-bearing stores are restricted to the Privacy Engineering role
   and require multi-party approval, recorded in the change register.
4. Daily backups are taken and restore tests are performed quarterly; results are recorded.
5. Object Lock in governance mode is applied to audit-log stores for the full retention period.

## 4. Secure disposal
At the end of the retention period information is disposed of by cryptographic erasure of the
managing key, followed by deletion of the objects. Disposal events are recorded in the retention
register with the class, the volume and the approver.
