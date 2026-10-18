# Backup Retention & Restore Validation

Backup policy must balance recovery, audit/compliance obligations, storage cost and customer-hosted operating constraints. Retention values are deployment policy, but backup classes and validation behavior are mandatory.

## Backup classes

| Class | Content | Protection |
|---|---|---|
| Transactional DB | customers/devices/entitlements/grants/deployments/config metadata | encrypted automated backup/PITR where supported |
| Audit | append-only audit/security records | protected backup/archive |
| Artifact repository | release/model binaries + immutable metadata references | versioning/replication/backup |
| Reconstruction config | deployment/application configuration excluding raw secrets | config management/protected backup |
| Secrets/certificates | app/service credentials | secret-manager/provider recovery |
| Signing keys | license/release/model key hierarchy | KMS/HSM/provider-specific protected recovery only |

## Retention baseline capability

Implementation SHALL support daily/weekly/monthly tiers and policy-specific extensions. Exact periods are finalized by operations/compliance/customer contract; the software/runbooks must not hard-code one universal retention duration.

Audit retention has its own configured policy (baseline 1–3 years) and is not implicitly equal to DB backup retention.

## Immutability/protection

Where available, critical backups use versioning/object lock/immutable backup controls appropriate to ransomware risk. Backup administrative access is separated from normal application credentials.

## Restore validation

A backup is not considered reliable until restore is tested. Exercises verify:
- DB integrity/schema compatibility
- tenant/customer ownership paths
- grant/allocation/audit continuity
- artifact hashes/manifests
- application startup/readiness
- secret/signing provider reconnection
- device check-in and safe signing in test scope
- worker/outbox duplicate safety

## Failure handling

Backup failure or stale backup age triggers operations alert. Failed restore exercise creates tracked remediation and may block production-readiness/DR claims.

## Evidence

Record backup ID/time/type, encryption/protection status, selected recovery point, restore environment, duration, validation checks, exceptions and remediation owner.

## Deletion

Expired backups are deleted through managed retention policy. Legal/security incident hold overrides normal deletion where formally applied.