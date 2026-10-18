# Database Design

~~~mermaid
erDiagram
    CUSTOMER ||--o{ SITE : owns
    CUSTOMER ||--o{ DEVICE : owns
    DEVICE }o--o{ SITE : assigned_to
    CUSTOMER ||--o{ ENTITLEMENT : owns
    ENTITLEMENT ||--o{ ALLOCATION : distributes
    ALLOCATION ||--o{ GRANT : produces
    DEVICE ||--o{ GRANT : receives
    DEVICE ||--o{ HARDWARE_INVENTORY : reports
    DEVICE ||--o{ RESOURCE_SNAPSHOT : reports
    DEVICE ||--o{ CAPACITY_ASSESSMENT : evaluated_by
    FEATURE ||--o{ FEATURE_RELEASE : versions
    MODEL ||--o{ MODEL_RELEASE : versions
    DEVICE ||--o{ DEVICE_MODEL_INVENTORY : has
~~~

Integrity rules: immutable IDs, FK constraints, UTC timestamps, strict tenant scoping, explicit grant supersession, idempotency constraints, transactional reallocation and audit events for sensitive mutations.