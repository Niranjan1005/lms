# Update Manager

The Update Manager is the only component allowed to commit application/feature/UI/runtime/model release sets on the edge.

## Transaction

~~~mermaid
flowchart TD
    A[Receive Deployment / Import Bundle] --> B[Validate Manifest Schema + Signature]
    B --> C[Validate Every Artifact Hash / Signature]
    C --> D[Check OS / Architecture / Runtime Compatibility]
    D --> E[Check License / Update Right]
    E --> F[Check Disk / Dependencies]
    F --> G[Local Capacity Preflight]
    G --> H[Preserve Known-Good Release Set]
    H --> I[Stage to Non-Active Location]
    I --> J[Run Signed Migration / Install Handlers]
    J --> K[Start / Restart Services]
    K --> L[Warm-up + Health Checks]
    L -->|Pass| M[Atomic Commit]
    L -->|Fail| N[Rollback Coherent Release Set]
    M --> O[Signed Installation Receipt]
    N --> O
~~~

## Preflight

Validate manifest version, target product/device, OS/architecture, source-version support, config schema, required runtime/model versions, disk space, grant/update rights, maintenance policy and local capacity.

## Staging and execution

- never execute directly from download/import media
- stage to dedicated path
- installation/migration handlers are signed artifacts referenced by manifest
- preserve previous known-good configuration/model set
- apply least required privilege
- make interrupted/restarted execution idempotent/recoverable

## Health checks

Health checks include process/service status plus product-specific readiness/warm-up. Merely starting a process is not a successful deployment.

## Rollback

Rollback restores application, plugins/features, UI/runtime, model versions and compatible configuration as one coherent release set. If rollback itself fails, emit critical failure receipt and require support/incident escalation.

## Download/import optimization

Compare installed artifact/model inventory and fetch/import only missing required content. Existing artifact content is reused only after hash/version validation.

## Receipt

Receipt records device, target release set, previous release set, grant revision, artifact/model versions, result, health outcome, rollback outcome and timestamps.