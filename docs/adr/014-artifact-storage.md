# ADR-014 — External Artifact Repository, PostgreSQL Metadata Only

**Status:** Approved  
**Decision class:** Storage / Release Architecture

## Context

Application/model binaries can be large and should not inflate transactional PostgreSQL storage/backups. SaaS and customer-hosted deployments need different storage providers while retaining common release metadata.

## Decision

PostgreSQL stores artifact metadata, references, hashes, signatures, compatibility and lifecycle state. Large binaries SHALL live in an artifact repository abstraction.

SaaS uses S3-compatible/object storage; customer-hosted uses MinIO or another approved repository/provider.

## Alternatives considered

### Store large binaries as PostgreSQL BLOBs
Rejected due to backup/restore growth and poor separation of transactional vs binary storage concerns.

### Hard-code one cloud object store
Rejected because customer-hosted/offline environments require provider flexibility.

## Consequences

- lighter transactional DB
- provider abstraction required
- artifact availability/backup monitored separately
- repository possession is not trust; devices still verify signature/hash

## Related requirements

`SDR-OTA-011`, `SDR-OPS-001`