# Usage Telemetry Schema

High-volume telemetry is logically separate from transactional licensing/audit data. Licensing decisions must not depend on best-effort analytics delivery unless a future approved design explicitly says otherwise.

## Telemetry families

- camera/input usage aggregates
- feature usage
- active hours
- inference counts
- performance/latency aggregates
- capacity/resource history
- trial activity aggregates
- runtime/application/model versions
- deployment health aggregates

## Common event envelope

~~~json
{
  "schema_version": 1,
  "event_id": "tel_...",
  "device_id": "dev_001",
  "customer_id": "cust_001",
  "site_id": "site_a",
  "event_type": "feature_usage_aggregate",
  "occurred_at": "2026-10-18T11:00:00Z",
  "period": {"start": "2026-10-18T10:00:00Z", "end": "2026-10-18T11:00:00Z"},
  "dimensions": {
    "feature_id": "ppe_detection",
    "app_version": "5.8.0",
    "model_version": "7.3.0"
  },
  "metrics": {
    "active_minutes": 55,
    "inference_count": 183240,
    "camera_count": 4
  }
}
~~~

## Schema rules

- version every event family
- timestamps in UTC
- event ID for deduplication
- customer/device/site attribution validated server-side against registered ownership
- additive evolution preferred; breaking changes create new schema/event version
- large arbitrary JSON payloads are avoided when stable typed dimensions/metrics exist

## Operational versus telemetry truth

Grant acceptance, installation receipt, entitlement mutation and privileged audit events remain transactional LMS records. Telemetry can copy/aggregate them for analytics but is not the sole source of operational truth.

## Storage

PostgreSQL remains the operational transactional store. High-volume telemetry should use a dedicated time-series/analytics/warehouse path when volume warrants it.

## Privacy boundary

Video/image content and personally identifying analytic payloads are not collected by default. Retention, opt-in/opt-out, residency and allowed customer-specific telemetry remain an explicit open product/security decision.