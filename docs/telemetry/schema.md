# Usage Telemetry Schema

High-volume telemetry is logically separate from transactional licensing data. Licensing decisions must not depend on best-effort analytics delivery unless explicitly designed.

## Planned telemetry families

- camera usage
- feature usage
- active hours
- inference counts
- trial activity
- capacity history
- runtime/application/model versions
- deployment health

## Event example

~~~json
{
  "event_id": "tel_...",
  "device_id": "dev_001",
  "site_id": "site_a",
  "feature_id": "ppe_detection",
  "event_type": "feature_usage_aggregate",
  "period": {"start": "2026-10-18T10:00:00Z", "end": "2026-10-18T11:00:00Z"},
  "metrics": {"active_minutes": 55, "inference_count": 183240, "camera_count": 4},
  "runtime": {"app": "5.8.0", "model": "7.3.0"}
}
~~~

## Architecture

Operational transactional DB remains PostgreSQL. Telemetry should move to a dedicated analytics/time-series/data-warehouse path when volume justifies it.

## Privacy open decision

Retention, customer opt-in/opt-out, data residency and personally identifiable data policy remain formal open decisions and must be resolved before production telemetry beyond operational necessity.