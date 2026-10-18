# Disaster Recovery & Continuity

Disaster recovery restores the control plane and its trust relationships without creating a second uncontrolled source of commercial/signing truth.

## Failure domains

DR planning covers:
- PostgreSQL loss/corruption
- LMS application/infrastructure loss
- artifact repository loss/corruption
- audit storage loss
- signing provider outage/region loss
- customer-hosted server loss
- credential/certificate loss
- ransomware/security incident requiring clean recovery

## Recovery dependencies

| Component | Recovery source | Special constraint |
|---|---|---|
| PostgreSQL | encrypted backups/PITR where supported | restore schema/business consistency |
| Artifact repository | versioning/replication/protected backup | verify hashes after restore |
| Audit data | protected backup/archive | preserve append-only evidence/identity |
| LMS config | reconstruction/config management | secrets restored separately |
| Signing metadata | PostgreSQL/config | private keys are separate |
| Signing private keys | KMS/HSM/provider recovery | never ordinary file/DB backup |
| Customer-hosted LMS | customer backup + signed install package | validate supported source/target versions |

## Recovery order

1. establish clean trusted infrastructure
2. restore database to selected recovery point
3. restore/attach artifact repository
4. restore non-secret configuration
5. restore/reconnect secrets and certificates through protected process
6. recover/reconnect signing provider independently
7. verify hashes/audit/schema/tenant authorization
8. start LMS read paths
9. validate signing using safe test scope
10. resume background jobs/outbox after duplicate/idempotency review
11. allow device check-ins/deployments
12. monitor reconciliation/backlog and communicate recovery status

## Recovery safety

- do not replay side effects blindly after DB restore
- inspect outbox/job states versus external systems
- ERP reconciliation detects commercial divergence
- devices may have accepted grant/release state newer than the restored central point; check-in/receipt reconciliation must handle this explicitly
- compromised signing key recovery follows security incident procedure, not normal DR

## RTO/RPO

Exact contractual enterprise RTO/RPO remain an open business/operations decision. Engineering SHALL measure database restore, artifact recovery, application restart, signing reconnection and reconciliation time before an SLA is promised.

## Mandatory exercises

- scheduled DB restore
- full LMS reconstruction
- artifact integrity verification
- schema migration + restored-data compatibility
- signing-provider recovery exercise without exposing raw private keys
- customer-hosted restore rehearsal
- worker/outbox duplicate-safety after recovery
- tabletop security/ransomware clean-room recovery

## DR evidence

Record scenario, recovery point, start/end time, measured data loss, component timings, validation checks, manual steps, failures and corrective owners.