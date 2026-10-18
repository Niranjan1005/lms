# Model OTA

AI models are first-class managed artifacts with independent identity, versioning, compatibility, encryption, deployment and rollback.

## Model release metadata

Each release records model ID/version, framework/backend, precision, input/output schema, feature compatibility, runtime range, accelerator/hardware compatibility, encrypted content hash, size, release channel and signing/encryption profile.

## Lifecycle

~~~mermaid
flowchart TD
    A[Create Model Release] --> B[Validate Metadata / Compatibility]
    B --> C[Encrypt Artifact with DEK]
    C --> D[Sign Manifest / Artifact]
    D --> E[Publish to Channel]
    E --> F[Resolve Authorized Target]
    F --> G[Compatibility + Capacity Check]
    G --> H[Download / Import Missing Content]
    H --> I[Verify Signature + Hash]
    I --> J[Authorize / Unwrap Content Key]
    J --> K[Stage Model]
    K --> L[Warm-up / Functional Health Check]
    L -->|Pass| M[Atomic Activate]
    L -->|Fail| N[Restore Previous Model]
~~~

## Independent OTA

A compatible model-only release may deploy without application redownload. The manifest must declare compatible feature/runtime ranges, and local inventory prevents redundant download.

## Authorization and encryption

Possessing the encrypted model file is not sufficient for use. The device needs both valid entitlement/grant authorization and authorized content-key unwrap/use according to the security model.

## Rollback

Previous known-good model remains available when storage permits. If application/plugin and model versions are tightly coupled, they are deployed/rolled back as one Release Set.

## Inventory

Edge reports model ID/version/hash/status. Central uses inventory for delta bundle generation and support visibility.

## Validation

Health/warm-up is model-specific and may include load success, inference sanity, expected output schema and latency/performance threshold. A hash-valid model that fails warm-up is not activated.

## Security boundary

No universal model password is permitted. Exact key wrapping/local secure storage follows ADR-009.