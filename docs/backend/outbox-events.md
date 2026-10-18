# Transactional Outbox & Internal Events

External side effects must not cause commercial/database state to become inconsistent when a network dependency fails.

## Pattern

For workflows such as grant signing, email delivery, ERP reconciliation and deployment dispatch:
1. commit business state and an outbox row in the same database transaction
2. background worker claims the outbox item
3. perform external action
4. persist success/failure and retry metadata
5. emit audit event

## Outbox schema baseline

~~~text
outbox_events
- event_id UUID/opaque ID
- aggregate_type
- aggregate_id
- event_type
- payload_json
- idempotency_key
- status: pending|processing|delivered|dead_letter
- attempt_count
- available_at
- created_at
- delivered_at
~~~

## Initial internal events

~~~text
device.registered
entitlement.created
entitlement.updated
allocation.changed
grant.issue_requested
grant.issued
grant.revoked
capacity.assessment_completed
trial.activated
renewal.approved
release.promoted
deployment.created
deployment.target_ready
installation.receipt_received
offline.response_ready
notification.requested
erp.reconciliation_required
~~~

## Delivery semantics

Use at-least-once internal delivery. Consumers must be idempotent. Event IDs and business idempotency keys prevent duplicate side effects.

## Dead-letter handling

Events exceeding retry policy move to `dead_letter`, trigger operations alerting and remain visible for manual recovery. They are never silently discarded.