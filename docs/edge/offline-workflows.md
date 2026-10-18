# Offline & Air-Gapped Workflows

Offline support is a first-class product path, not an exception.

## Request package contains

- request_id and nonce
- device identity/public-key reference
- current grant revisions
- installed release/model inventory
- hardware inventory version and relevant workload
- requested operation: activation, trial, renewal, release update, model update
- device signature over canonical request payload

## Response package contains

- request_id/nonce binding
- signed grant revision(s) where applicable
- release-set manifest
- only required/missing artifacts
- encrypted model artifacts if required
- signatures/hashes
- expiry/import policy

## Local import order

~~~mermaid
flowchart TD
    A[Read Package] --> B[Verify package signature/hash]
    B --> C[Verify request_id + nonce binding]
    C --> D[Verify device/product scope]
    D --> E[Reject replay / stale revision]
    E --> F[Resolve grant and dependencies]
    F --> G[Capacity re-check]
    G --> H[Stage release set]
    H --> I[Health check]
    I -->|Pass| J[Commit + activate]
    I -->|Fail| K[Rollback]
    J --> L[Generate signed receipt]
~~~

Revocation cannot be instantaneous on a fully air-gapped device; it becomes effective when new signed state is imported or when existing offline authorization expires.