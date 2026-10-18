# Edge / Application Engineering

The edge is the enforcement and execution boundary. Central LMS decides commercial policy and issues signed state; the edge decides whether that signed state is valid for the actual device, runtime and workload.

## Core components

| Component | Responsibility |
|---|---|
| Device Identity Agent | key lifecycle, fingerprint evidence, enrollment identity |
| Hardware Inventory Agent | stable hardware/runtime inventory and dynamic snapshots |
| License Agent | signed grant verification and runtime authorization |
| Local Capacity Engine | authoritative combined-workload feasibility check |
| Update Manager | package/model verification, staging, migration, health and rollback |
| Product Adapter / Analytics Runtime | enforce License Agent decisions at actual feature/workload boundaries |
| Offline Exchange | signed request/response import/export and receipt queue |

## Local trust flow

~~~mermaid
flowchart LR
    ID[Device Identity] --> LA[License Agent]
    INV[Inventory / Workload] --> CAP[Local Capacity]
    UM[Update Manager] --> RT[Runtime]
    LA --> RT
    CAP --> RT
    RT --> REC[Receipts / Check-ins]
~~~

## Edge invariants

1. No protected feature executes solely because a UI toggle is enabled.
2. License Agent authorization is checked at runtime/workload boundaries.
3. Local capacity is authoritative for activation.
4. Update Manager is the only component that commits a Release Set.
5. Invalid/tampered packages never become active.
6. Central unavailability does not break a still-valid offline authorization.
7. Anti-replay/revision/trusted-time state survives service restart.
8. Recovery/import/diagnostic functions remain available where safe when analytics are restricted.

## Connectivity modes

The same edge components support direct online sync, assisted relay and fully air-gapped controlled-media exchange. Transport changes; signature, binding and local verification semantics do not.

## Platform abstraction

Linux is first. Local interfaces, key-storage abstraction, package handlers and service control are designed so Windows-native implementations can be added without changing central licensing semantics.

## Related SDR

`SDR-DEV-*`, `SDR-CAP-*`, `SDR-OFF-*`, `SDR-OTA-*`, `SDR-SEC-*`