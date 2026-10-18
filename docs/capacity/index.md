# Capacity Management

Capacity management answers **what this hardware can run at the target performance**, independently from what the customer commercially owns.

## Four independent states

A feature/device combination must keep these states separate:

1. **Licensed** — commercial right exists.
2. **Compatible** — OS/runtime/hardware/dependency requirements are satisfied.
3. **Capacity Validated** — combined workload meets the performance target or an approved warning policy.
4. **Installed / Healthy** — required application/model components are installed and healthy.

A feature activates only when all required gates pass.

## Authority model

**Central Capacity Engine** performs advisory pre-assessment using reported inventory, workload definitions and approved benchmark profiles.

**Local Capacity Engine** performs the authoritative activation check using current drivers, resources, active streams, installed versions and actual local runtime conditions.

## Core process

~~~mermaid
flowchart LR
    A[Collect stable inventory] --> B[Check compatibility]
    B --> C[Describe current + proposed workloads]
    C --> D[Select approved benchmark profiles]
    D --> E[Calculate combined resource budget]
    E --> F[Compare against target/headroom policy]
    F --> G{PASS / WARNING / FAIL}
    G -->|PASS| H[Recommend activation]
    G -->|WARNING| I[Recommend constrained configuration]
    G -->|FAIL| J[Recommend alternatives / hardware change]
    H --> K[Local authoritative recheck]
    I --> K
    J --> K
    K --> L[Monitor runtime and reassess on change]
~~~

## Non-negotiable rules

- Capacity never silently reduces purchased entitlement.
- Licensed camera/feature quantity is not itself a capacity calculation.
- Existing and proposed workloads are evaluated together.
- Central advice may become stale; local activation remains authoritative.
- Capacity recommendations are explicit and operator-selectable.
- Benchmark evidence is versioned and governed.
- Runtime changes can invalidate an old assessment.