# Database Design

PostgreSQL stores transactional LMS business truth. The schema separates commercial rights, device identity, runtime evidence, release/deployment state and audit rather than collapsing them into one device record.

## Core relationships

~~~mermaid
erDiagram
    CUSTOMER ||--o{ SITE : owns
    CUSTOMER ||--o{ DEVICE : owns
    DEVICE ||--o{ DEVICE_SITE_ASSIGNMENT : has
    SITE ||--o{ DEVICE_SITE_ASSIGNMENT : has
    CUSTOMER ||--o{ ENTITLEMENT : owns
    ENTITLEMENT ||--o{ ENTITLEMENT_ITEM : contains
    ENTITLEMENT_ITEM ||--o{ ALLOCATION : distributes
    DEVICE ||--o{ ALLOCATION : receives
    ENTITLEMENT ||--o{ GRANT : derives
    DEVICE ||--o{ GRANT : receives
    DEVICE ||--o{ HARDWARE_INVENTORY : reports
    DEVICE ||--o{ RESOURCE_SNAPSHOT : reports
    DEVICE ||--o{ CAPACITY_ASSESSMENT : evaluated_by
    FEATURE ||--o{ FEATURE_RELEASE : versions
    MODEL ||--o{ MODEL_RELEASE : versions
    DEPLOYMENT_JOB ||--o{ DEPLOYMENT_TARGET : targets
    DEVICE ||--o{ INSTALLATION_RECEIPT : reports
~~~

## Data-domain rules

### Identity/topology
Customer owns sites and devices. Device-site relationships are explicit assignments so one device may serve multiple sites without changing commercial ownership.

### Commercial licensing
Entitlement/entitlement items define purchased rights. Allocations distribute pooled quantity. Grants are signed device-bound runtime artifacts derived from entitlement/allocation/policy.

### Capacity evidence
Stable hardware inventory, dynamic resource snapshots, workload profiles, benchmark profiles and capacity assessments are distinct tables/records so assessments remain reproducible.

### Release/deployment
Feature/model releases and artifact metadata are immutable after publication. Deployment job is central orchestration state; installation receipt is device evidence.

### Audit/integration
Audit events are append-only. ERP/outbox/idempotency records support safe integration/retry without changing commercial truth silently.

## Integrity requirements

- immutable opaque IDs
- foreign keys for ownership/lineage
- UTC timestamps
- tenant/customer ownership path on business data
- check/unique constraints for invariants where possible
- optimistic revision on mutable aggregates
- explicit grant supersession
- transactional allocation/reallocation
- unique idempotency key + request hash
- append-only audit semantics

## Transaction boundaries

One business transaction is used for entitlement allocation changes, grant supersession metadata, decommission + allocation return, approval execution and other operations where partial DB success would violate commercial truth.

External signing/storage/email/ERP calls do not run as fake distributed transactions; the outbox/job pattern bridges those boundaries.

## JSON usage

JSON columns are permitted for bounded/extensible evidence and policy attributes such as hardware details or reason lists, but core ownership, quantities, revisions, statuses and relationships remain relational.

## Migration principles

Alembic is the only supported migration path. Risky changes use expand-and-contract. Customer-hosted upgrade manifests declare supported source schema/app versions.

## Performance/indexing

Indexes follow real access patterns such as tenant+status, device+time, grants by device/status/expiry, deployment target status and audit time/object lookups. Final indexes are verified using production-like plans and scale tests.

## Related SDR

`SDR-BE-003`, `SDR-BE-005`, `SDR-BE-009`, `SDR-OPS-001`