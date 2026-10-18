# Telemetry Delivery, Buffering & Retention

Telemetry is best-effort operational/analytics data unless a specific event is also persisted transactionally in LMS.

## Edge delivery

- aggregate where possible before upload
- batch and compress to reduce bandwidth
- support bounded local buffering during offline periods
- retry transient failures with backoff
- never allow telemetry backlog to consume unbounded disk
- discard/roll up lowest-value historical telemetry according to policy before affecting core product operation

## Ordering and deduplication

Events carry event ID, device ID and event timestamp. Central ingestion is idempotent where duplicate delivery is possible. Analytics pipelines must tolerate delayed/out-of-order events.

## Connectivity modes

Connected devices may stream/batch periodically. Assisted-offline/air-gapped telemetry export is optional and must be explicitly designed; licensing does not depend on high-volume telemetry being returned.

## Retention

Operational capacity/deployment evidence needed for licensing/support remains in transactional records according to audit/support policy. High-volume telemetry uses a separate retention policy/storage tier.

## Privacy

Do not collect video/image content or personally identifying analytics payloads by default unless separately approved. Telemetry privacy, residency and opt-in/opt-out remain an open product/security decision.