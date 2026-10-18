# Architecture Overview

The LMS is a modular enterprise control plane. Business truth is centralized; final authorization and installation enforcement remain local.

~~~mermaid
flowchart TB
    P[Admin / Customer Portal] --> API[Central LMS API]
    API --> REG[Registry & Enrollment]
    API --> ENT[Entitlement Engine]
    API --> POL[Policy Engine]
    API --> CAP[Capacity Service]
    API --> MKT[Marketplace]
    API --> REL[Release / OTA]
    API --> LIFE[Lifecycle / Renewal]
    API --> AUD[Audit & Reporting]
    ENT --> SIGN[Protected Signing Service]
    POL --> SIGN
    REL --> AR[(Artifact Repository)]
    API --> DB[(PostgreSQL)]
    API -->|Online| EDGE[Edge / Server]
    API -->|Signed request-response| RELAY[Authorized Relay]
    RELAY --> EDGE
    EDGE --> ID[Device Identity]
    EDGE --> LA[License Agent]
    EDGE --> LC[Local Capacity Engine]
    EDGE --> UM[Update Manager]
    EDGE --> RT[Analytics Runtime]
~~~

## Responsibility split

- Entitlement Engine: what the customer owns.
- Policy Engine: under what conditions it may be used.
- Capacity Engine: what the hardware can run safely.
- Release/OTA: which software/model artifacts are installed.
- License Agent: whether the feature may execute.