# OpenAPI Schema Baseline

This page defines canonical payload shapes that backend and edge teams should treat as the starting contract before generated OpenAPI is frozen.

## Common identifiers

All identifiers are opaque strings with stable prefixes. Examples: `cust_`, `site_`, `dev_`, `ent_`, `alloc_`, `grant_`, `rel_`, `mr_`, `dep_`. Clients must not infer meaning from ID structure beyond object type.

## Pagination

~~~json
{
  "data": [],
  "meta": {
    "request_id": "req_...",
    "next_cursor": "opaque-or-null",
    "page_size": 100
  }
}
~~~

## Device registration request

~~~json
{
  "enrollment_token": "opaque",
  "product_id": "prod_analytics",
  "device_identity": {
    "public_key": "base64-or-pem",
    "algorithm": "ed25519",
    "fingerprint": {"version": 1, "hash": "sha256:..."}
  },
  "hardware_inventory": {
    "schema_version": 1,
    "cpu": {"model": "...", "physical_cores": 8, "logical_cores": 16},
    "memory": {"total_mb": 32768},
    "gpu": [{"vendor": "nvidia", "model": "...", "vram_mb": 12288}],
    "storage": [{"mount": "/", "total_mb": 500000, "free_mb": 200000}],
    "os_runtime": {"os": "ubuntu", "version": "24.04", "kernel": "...", "cuda": "..."}
  }
}
~~~

## Device registration response

~~~json
{
  "data": {
    "device_id": "dev_123",
    "registration_state": "registered",
    "license_state": "not_licensed",
    "capacity_state": "not_assessed",
    "checkin_policy": {"offline_days": 7}
  },
  "meta": {"request_id": "req_...", "api_version": "v1"}
}
~~~

## Entitlement create/update model

~~~json
{
  "customer_id": "cust_100",
  "product_id": "prod_analytics",
  "term": {
    "type": "subscription",
    "starts_at": "2026-01-01T00:00:00Z",
    "expires_at": "2026-12-31T23:59:59Z"
  },
  "items": [
    {
      "feature_id": "ppe_detection",
      "quantity": {"type": "camera_count", "value": 40},
      "update_policy": {"mode": "during_active_term"}
    }
  ]
}
~~~

## Allocation request

~~~json
{
  "expected_entitlement_revision": 12,
  "changes": [
    {"device_id": "dev_a", "feature_id": "ppe_detection", "quantity": 8},
    {"device_id": "dev_b", "feature_id": "ppe_detection", "quantity": 20},
    {"device_id": "dev_c", "feature_id": "ppe_detection", "quantity": 8}
  ],
  "reason": "customer workload rebalance"
}
~~~

Allocation is validated and committed as one business operation. Result contains new entitlement/allocation revisions and affected grant issuance status.

## Check-in request

~~~json
{
  "device_id": "dev_123",
  "accepted_grants": [{"grant_id": "grant_1", "revision": 8}],
  "active_release_set_id": "rs_001",
  "model_inventory": [{"model_id": "ppe_detector", "version": "7.3.0"}],
  "last_trusted_time": "2026-10-18T11:00:00Z",
  "health": {"status": "healthy"}
}
~~~

## API compatibility rule

Within `/v1`, additive fields are allowed, removal/semantic repurposing is not. Breaking changes require a new API version or a documented migration window.