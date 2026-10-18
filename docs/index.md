# LMS Engineering Handbook

> Internal source of truth for the License, Marketplace & Edge Lifecycle Management Platform.

<div class='grid cards' markdown>

-   :material-sitemap:{ .lg .middle } **Architecture**

    ---

    Control plane, trust boundaries, SaaS/on-prem deployment and online/offline/air-gapped operation.

    [Architecture](architecture/index.md)

-   :material-key-chain:{ .lg .middle } **Licensing**

    ---

    Entitlement pools, allocations, device-bound grants, trials, renewal, grace and offline validity.

    [Licensing](licensing/index.md)

-   :material-store-cog:{ .lg .middle } **Marketplace & OTA**

    ---

    Feature discovery, trial/purchase, release channels, traditional packages, model OTA and rollback.

    [Marketplace & OTA](marketplace-ota/index.md)

-   :material-server-security:{ .lg .middle } **Backend Engineering**

    ---

    FastAPI modular monolith, PostgreSQL, API standards, audit and signing integration.

    [Backend](backend/index.md)

</div>

## Platform mission

**Make enterprise AI deployments — including offline and air-gapped environments — scalable, governable and monetizable.**

~~~mermaid
flowchart LR
    A[Customer & Device Registry] --> B[Entitlements]
    B --> C[Policy Engine]
    C --> D[Device-bound Grants]
    A --> E[Hardware & Capacity]
    D --> F[Marketplace]
    E --> F
    F --> G[Release / OTA]
    G --> H[Edge Runtime]
    H --> I[Telemetry / Audit]
    I --> J[Renewal / Lifecycle]
~~~

## Approved principles

- Registration, licensing and capacity validation are separate states.
- Commercial rights are central entitlements; executable permissions are device-bound signed grants.
- Customer rights may be pooled and reallocated, while grants remain device-bound.
- The same trust model supports online, assisted-offline and fully air-gapped operation.
- Marketplace and OTA live inside LMS because they use the same customer, device, entitlement, capacity and release data.
- Automatic updates consume Stable releases by default; LTS is explicitly controlled by the company.
- Model files are independently versioned, encrypted, signed, inventory-aware and rollback-capable.
- Capacity assessment recommends feasible deployment and never silently reduces purchased rights.