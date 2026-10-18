# Artifact Storage Architecture

PostgreSQL stores transactional metadata, references, hashes, signatures, compatibility and deployment state. Large application/model binaries must not be stored as normal PostgreSQL blobs.

## Storage abstraction

~~~text
Release / Model Service
        ↓
Artifact Repository Interface
        ├── SaaS: S3-compatible object storage
        └── Customer-hosted: MinIO or approved local repository
~~~

## Stored metadata

Database records include artifact ID, release/model association, URI/reference, size, content hash, signature/key ID, encryption profile, creation/publish state and retention metadata.

## Integrity

Artifact bytes are immutable after publication. Replacement requires a new artifact/release identity. The edge verifies manifest signature and content hash before installation/decryption.

## Signing separation

Artifact storage is not a signing authority. Signing keys remain in the protected signing boundary; the repository stores only signed outputs and verification metadata.