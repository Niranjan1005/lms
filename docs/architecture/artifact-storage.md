# Artifact Storage Architecture

PostgreSQL stores transactional metadata and lifecycle state. Large application, UI, dependency and encrypted model binaries live in an external artifact repository through a provider abstraction.

## Storage abstraction

~~~text
Release / Model Service
        ↓
Artifact Repository Interface
        ├── SaaS: S3-compatible object storage
        └── Customer-hosted: MinIO / approved filesystem-object provider
~~~

## Responsibilities

### PostgreSQL
Stores artifact ID, release/model association, logical type, immutable version, repository reference, size, content hash, signature/key ID, encryption profile, compatibility, publish/retire state and audit linkage.

### Artifact repository
Stores immutable binary bytes and supports controlled put/get/head, retention/versioning/backup according to provider capability.

### Signing provider
Signs manifests/artifacts or hashes according to release format. Artifact storage itself never possesses signing authority.

## Publication flow

1. upload/stage candidate bytes
2. validate size/type/security constraints
3. compute content hash
4. create release/model metadata
5. build canonical manifest
6. obtain protected signature
7. mark artifact/release Published atomically at metadata level
8. published bytes become immutable

## Immutability

A Published artifact is never replaced in place. Correction creates a new artifact/release identity/version. Repository object versioning may retain old bytes but LMS lifecycle state governs new deployment eligibility.

## Integrity and download

Edge trusts the signed manifest and expected content hash, not repository location. Downloaded/imported bytes are verified before install/decryption. Existing local content is reused only when identity/version/hash match.

## Access control

Central service uses least-privilege repository credentials. Pre-signed/temporary URLs, if used, are short-lived and scoped. Direct bucket/container listing is not a customer authorization mechanism.

## Encryption

Provider-side encryption at rest is used where supported. Model artifacts additionally use application-level model encryption according to the model protection design.

## Retention and deletion

Retired releases may be retained for rollback/support/DR according to policy. Deletion must not remove content still referenced by supported releases, active deployments or required rollback sets.

## Backup/DR

Repository backup/versioning/replication is tested together with PostgreSQL metadata recovery. Restore validation verifies hashes and referential availability.

## Related SDR/ADR

`SDR-OTA-006`, `SDR-OTA-011`, `SDR-OPS-001`; ADR-014