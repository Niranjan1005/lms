# Model OTA

AI models are first-class managed artifacts with identity, semantic version, framework/runtime, hardware compatibility, precision, encrypted hash, size, release channel and feature compatibility.

~~~mermaid
flowchart TD
    A[Publish Model Release] --> B[Validate Metadata]
    B --> C[Encrypt Artifact]
    C --> D[Sign Artifact / Manifest]
    D --> E[Assign Channel]
    E --> F[Resolve Target Devices]
    F --> G[Compatibility + Capacity Check]
    G --> H[Download / Import]
    H --> I[Verify Signature + Hash]
    I --> J[Authorize Decryption]
    J --> K[Stage Model]
    K --> L[Warm-up / Health Check]
    L -->|Pass| M[Activate]
    L -->|Fail| N[Rollback]
~~~

If a required model already exists locally, it must not be downloaded again.