# Update Manager

~~~mermaid
flowchart TD
    A[Receive Release Set] --> B[Verify Signatures & Hashes]
    B --> C[Check OS / Architecture]
    C --> D[Check Disk / Dependencies]
    D --> E[Check License]
    E --> F[Check Capacity]
    F --> G[Preserve Known-Good Version]
    G --> H[Stage]
    H --> I[Run Migrations]
    I --> J[Restart Services]
    J --> K[Health Check]
    K -->|Pass| L[Commit]
    K -->|Fail| M[Rollback]
~~~

No normal production release should depend on manual site migration.