# Customer-Hosted Deployment Topology

Customer-hosted LMS uses the same application codebase with deployment-mode configuration.

## Baseline topology

~~~mermaid
flowchart TB
    U[Customer/Vendor Admin Browser] --> RP[Reverse Proxy / TLS]
    RP --> LMS[LMS Application]
    LMS --> PG[(PostgreSQL)]
    LMS --> AR[(Artifact Repository / MinIO or approved storage)]
    LMS --> SG[Signing Gateway / configured secure provider]
    LMS --> SMTP[SMTP / notification relay]
    EDGE[Edge Devices] <--> LMS
~~~

## Minimum production requirements

- TLS termination
- persistent PostgreSQL storage
- persistent artifact storage
- backup destination
- secrets/configuration outside source code
- monitoring/log export
- time synchronization
- outbound email if notifications are enabled

## Upgrade model

Customer-hosted LMS self-update is manual in the initial product. Vendor supplies a signed LMS release package/runbook; customer/operator executes upgrade within an approved maintenance window.

## HA

HA is an enterprise option rather than mandatory Phase 1 baseline. Exact topology and RTO/RPO are decided per deployment tier.