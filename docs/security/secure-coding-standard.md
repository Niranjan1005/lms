# Secure Coding Standard

This standard applies to backend, portal, edge agents, update tooling, offline package parsers and administrative utilities.

## Input validation

- treat API, ERP, device, file, manifest and offline-package input as untrusted
- validate type, length, range, enum, encoding and cross-field invariants
- define maximum body/upload/archive sizes
- reject unknown security-critical fields in canonical signed payload formats
- prevent mass-assignment of protected fields
- do not trust client-provided tenant/role/status fields

## File/archive/package handling

- extract only into a dedicated staging directory
- normalize and validate every path before write
- reject traversal, absolute paths, device paths and symlink/hardlink escapes
- cap expanded bytes, file count, nesting depth and compression ratio
- reject unsigned/unreferenced executable scripts
- verify manifest signature and hashes before install
- never execute directly from upload/temp location
- clean failed/quarantined content according to policy

## Authentication and authorization

- authenticate before authorization
- enforce permission + object scope at business-service boundary
- deny by default
- never rely on hidden buttons/routes for security
- prevent IDOR/BOLA by ownership validation for every object reference
- service/background identities use least privilege
- privileged reprocessing/override operations are separately authorized

## Database

- parameterized ORM/query use
- no string-concatenated SQL with untrusted input
- explicit transaction boundaries
- optimistic concurrency for mutable aggregates
- tenant predicates/ownership joins are mandatory
- DB errors are mapped to safe application errors
- migrations reviewed for locking/data-loss implications

## API and web security

- strict content type
- secure headers
- CSRF protection for cookie-based state changes
- CORS allowlist
- rate limits for abuse-prone endpoints
- pagination/bounds on expensive queries
- request correlation ID
- avoid reflecting untrusted HTML/script content
- protect download/export endpoints with the same authorization as source records

## Cryptography

- approved library/provider only
- no home-grown crypto
- CSPRNG for tokens/nonces/keys
- use library-provided safe secret/token comparison primitives
- signature verification fails closed
- explicit algorithm/key ID/canonicalization version
- never reuse signing keys for unrelated purposes

## Error handling

- never return stack traces, SQL errors, secret values or internal filesystem paths to clients
- security-sensitive errors may be externally generalized
- secure logs retain investigation correlation
- retryability is explicit

## Logging

Allowed: request ID, safe actor/object IDs, action/result, error code and timings.

Forbidden in normal logs: passwords, bearer/refresh tokens, enrollment secrets, private keys, unwrapped DEKs, decrypted model bytes and sensitive raw signed payloads.

## Concurrency and idempotency

Security-sensitive writes use idempotency and/or optimistic revision checks where duplicate or replay execution would be dangerous.

## Dependency use

- pin/constraint production dependencies
- review purpose/maintenance posture of new high-risk dependencies
- SCA in CI
- remove unused dependencies
- never dynamically download and execute code from untrusted locations in production

## Required negative tests

Parser/authz/crypto boundaries include tests for tampered signature, wrong tenant, wrong device, stale revision, replayed nonce, malformed archive, traversal path, oversized input and unknown critical schema fields.