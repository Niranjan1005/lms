# Background Jobs & Scheduler

Background execution is a first-class backend subsystem with durable, idempotent jobs.

## Job families

- renewal reminders
- trial expiry processing
- stale offline-check-in detection
- grace/restriction transitions
- grant delivery/reconciliation retries
- notification delivery
- ERP reconciliation
- deployment orchestration and rollout scheduling
- artifact retention/cleanup
- telemetry aggregation/export
- audit retention/export
- capacity reassessment requests triggered by reported changes

## Reliability rules

- Jobs are idempotent.
- Durable job state survives application restart.
- Retryable failures use bounded exponential backoff.
- Non-retryable validation/security failures enter failed/dead-letter state.
- A job records customer/tenant scope explicitly.
- Duplicate execution must not issue duplicate grants or double-apply entitlement changes.
- Jobs that cause external side effects use the transactional outbox pattern where appropriate.

## Scheduling

Time-based jobs use UTC internally. Customer/site timezone is applied for maintenance windows and user-facing schedules.

## Observability

Expose queue depth, oldest-pending age, success/failure/retry rate and dead-letter count per job family.

## Operational ownership

Support/operations can retry or cancel only approved job classes. Privileged reprocessing that can alter commercial/license state is audited and may require approval.