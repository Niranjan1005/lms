# Backup & Recovery

Backup/recovery protects business truth, deployment evidence and artifact availability without treating signing private keys as normal application data.

## Backup scope

- PostgreSQL transactional state
- audit data
- artifact metadata and release/model manifests
- artifact repository binaries or replicated/versioned equivalent
- deployment/configuration reconstruction metadata
- operational configuration templates that do not contain raw secrets

Signing private keys use a separate KMS/HSM/provider recovery mechanism and are never copied into ordinary DB/file backups.

## SaaS Phase 1 baseline

- automated encrypted database backups
- point-in-time recovery where chosen PostgreSQL platform supports it
- object/artifact versioning or protected backup
- backup job monitoring/alerting
- documented restore procedure
- regular restore exercise
- single-primary acceptable initially while remaining HA-ready

## Customer-hosted baseline

Installation package defines what the customer must back up, supported backup commands/provider integration, required artifact/config directories and restore ordering.

## Restore order

1. establish clean supported LMS environment
2. restore PostgreSQL
3. restore/attach artifact repository
4. restore non-secret configuration/reconstruction metadata
5. reconnect protected signing provider using its independent process
6. run integrity/migration compatibility validation
7. verify tenant/authz/audit state
8. verify device check-in and safe signing integration

## Integrity checks

Restore validation checks DB consistency, schema version, artifact hashes, manifest availability, audit continuity, application startup and tenant scoping.

## Recovery evidence

Record backup identifier/time, recovery point, operator, restore duration, verification checks, exceptions and remediation.

## Open decision

Exact contractual RPO/RTO remains an enterprise operations decision. Engineering must measure restore performance before any promise is made.