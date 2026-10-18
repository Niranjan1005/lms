# Database Indexing, Transactions & Concurrency

Tier-1 reliability depends on explicit concurrency behaviour, not only schema shape.

## Transaction boundaries

Use one database transaction for operations where partial success would violate commercial truth, including:
- entitlement-pool reallocation across multiple devices
- grant revision + supersession record creation
- renewal term update + grant issuance record preparation
- device decommission + allocation return
- approval execution state transitions

External calls such as signing and artifact storage should use an outbox/saga-style pattern when they cannot participate in the DB transaction.

## Optimistic concurrency

Mutable aggregates carry `revision` or `version`. Update commands include expected revision. A mismatch returns a conflict rather than overwriting concurrent changes.

## Initial index strategy

- unique(customer_id, external_reference) where integration keys apply
- unique(device_id, active key status constraint)
- index(customer_id, status) on customer-scoped collections
- index(device_id, collected_at desc) for inventory/snapshots
- unique(entitlement_id, feature_id, active pool identity) as model permits
- index(grants: device_id, status, valid_until)
- unique(grant_id, revision)
- index(capacity_assessments: device_id, assessed_at desc)
- unique(feature_id, version) and unique(model_id, version)
- index(deployment_targets: job_id, status)
- index(audit_events: customer_id, occurred_at desc) and object lookup indexes

Exact indexes must be validated against production-like query plans before launch.

## Idempotency storage

Persist key, operation, request hash, response reference, created_at and expiry. Same key + different request hash is rejected.