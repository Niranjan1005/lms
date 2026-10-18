# Telemetry Delivery, Buffering & Retention

Telemetry is best-effort operational/analytics data unless an event is separately persisted as transactional LMS state. Its delivery path must not threaten core edge operation or license validity.

## Edge buffering

- aggregate high-frequency events where possible
- batch/compress uploads
- keep a bounded disk quota for telemetry queue
- use append/queue format resilient to restart
- retry transient network/server failures with backoff
- prioritize recent/important operational aggregates over low-value historical detail when buffer pressure occurs
- never consume disk reserved for application rollback/license recovery

## Delivery envelope

Each batch/event carries schema version, event ID, device/customer/site identity, occurred/period time and payload metrics. Central validates ownership and schema before accepting.

## Deduplication and ordering

Central ingestion uses event ID/batch identity for idempotency. Analytics tolerates delayed and out-of-order events because offline devices may upload much later.

## Connectivity modes

### Connected
Periodic batch/stream according to bandwidth policy.

### Assisted offline / air-gapped
High-volume telemetry return is optional. If enabled, it uses explicit export/import packages separate from mandatory license/update receipts. Licensing must remain functional without telemetry export.

## Backpressure

If central ingestion is unavailable or slow, edge reduces retry frequency and keeps bounded local data. Telemetry failure must not cause analytics runtime/license agent/update manager failure.

## Storage separation

Operational transactional evidence such as installation receipts, accepted grant revisions and audit events remains in LMS PostgreSQL. High-volume telemetry uses a separate analytics/time-series/warehouse path as scale requires.

## Retention

Retention is policy by event family/customer/regulatory need. Operational support evidence may have longer retention than raw high-volume metrics. Exact privacy/retention/residency values remain an open decision.

## Privacy/data minimization

Do not collect video/image content or person-identifying analytic payloads by default. Prefer aggregate counts/performance metrics. New sensitive telemetry requires explicit product/security/privacy review.

## Observability

Monitor ingest error rate, queue age, dropped/rolled-up events, device buffer pressure and schema rejection. These metrics diagnose telemetry quality, not commercial license state.

## Related SDR

`SDR-TEL-001` through `SDR-TEL-003`