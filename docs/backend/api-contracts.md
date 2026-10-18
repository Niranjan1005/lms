# API Contract Baseline

API contracts are versioned, explicit and backward-compatible within a major version. The examples below are implementation baselines, not final generated OpenAPI.

## Common headers

~~~text
Authorization: Bearer <token>
X-Request-ID: <uuid>
Idempotency-Key: <uuid>    # required on retryable write workflows
~~~

## Standard success envelope

~~~json
{
  "data": {},
  "meta": {"request_id": "req_...", "api_version": "v1"}
}
~~~

## Register device

`POST /v1/devices/register`

~~~json
{
  "enrollment_token": "...",
  "product_id": "prod_100",
  "device_public_key": "...",
  "fingerprint": {"version": 1, "hash": "..."},
  "network_evidence": {"mac_addresses": ["..."]},
  "hardware_inventory": {"schema_version": 1, "cpu": {}, "gpu": {}, "memory": {}, "storage": {}, "os_runtime": {}}
}
~~~

Response state must distinguish `registered`, `licensed` and `capacity_validated`.

## Capacity assessment

`POST /v1/devices/{device_id}/capacity-assessments`

~~~json
{
  "existing_workloads": [{"feature_id": "people_counting", "cameras": 8, "fps": 10}],
  "proposed_workloads": [{"feature_id": "ppe", "cameras": 4, "fps": 10}],
  "resource_snapshot_id": "snap_123"
}
~~~

~~~json
{
  "data": {
    "result": "warning",
    "recommended_options": [
      {"type": "reduce_active_cameras", "feature_id": "ppe", "value": 2},
      {"type": "move_workload", "target": "another_device"}
    ],
    "benchmark_profile_version": "bp-2026.10"
  }
}
~~~

## Grant issuance

`POST /v1/grants/issue` is privileged/internal. It consumes an approved entitlement/allocation/policy snapshot and must be idempotent. Direct client-supplied limits are not trusted without policy validation.

## Offline exchange

`POST /v1/offline/requests/import` validates request ID, nonce, device signature, device ownership and request age before any grant/package generation.

## Installation receipt

`POST /v1/installations/receipts` records package/model versions, hashes, health result, rollback status and accepted grant revision.