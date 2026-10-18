# Device-Bound Grants

A grant is the signed executable permission derived from approved entitlement, allocation and resolved policy. It is not the commercial contract itself.

## Required grant content

A production grant carries at minimum:
- schema/canonicalization version
- grant ID and revision
- superseded grant lineage
- issue timestamp
- customer/product/device subject
- one or more capabilities
- quantity/site/model/runtime constraints
- commercial term
- offline freshness and grace policy
- dependencies
- update-right policy where applicable
- signing key ID/algorithm
- signature

## Illustrative grant

~~~json
{
  "schema_version": 1,
  "grant_id": "grant_1001",
  "revision": 8,
  "supersedes": "grant_0988",
  "subject": {
    "customer_id": "cust_100",
    "product_id": "ai_box",
    "device_id": "dev_310"
  },
  "capabilities": [{
    "code": "ppe_detection",
    "limits": [{"key": "camera_count", "op": "lte", "value": 4}],
    "dependencies": [{"capability": "analytics_base", "required": true}]
  }],
  "commercial": {"type": "subscription", "valid_until": "2027-10-31T23:59:59Z"},
  "runtime": {"offline_days": 7, "grace_days": 7},
  "key_id": "lic_sign_01",
  "algorithm": "ed25519",
  "signature": "base64..."
}
~~~

## Issuance rules

Grant issuance SHALL:
1. resolve current entitlement/allocation/policy
2. validate tenant/device ownership
3. validate pooled quantity invariant
4. calculate revision/supersession
5. persist issuance intent and audit state
6. obtain signature from protected signing service
7. persist signed artifact metadata
8. deliver online or through offline response flow

Direct client-provided limits are not trusted without policy/entitlement validation.

## Acceptance rules

Edge accepts a grant only after verifying:
- trusted key ID and signature
- canonical payload integrity
- customer/product/device binding
- valid-from/valid-until
- revision and supersession
- dependency constraints
- current trusted time
- local quantity/site scope
- relevant compatibility/capacity/install state

## Supersession

Replacement grant revisions SHALL not be aggregated with superseded versions. Edge persists the highest accepted revision per lineage and rejects rollback unless an explicit signed recovery mechanism exists.

## Delivery state

`Issued`, `Delivered/Imported` and `Accepted/Active` are separate states. Central issuance alone is not evidence that an offline device is using the new rights.

## Perpetual/update rights

Perpetual grants can carry explicit update-right policies such as `unlimited`, `during_active_term`, `remaining_major_updates`, `until_version` or `none`.

## Failure handling

Signing failure leaves issuance pending/retryable through durable jobs/outbox. Invalid or rejected grants never replace a previously valid accepted grant unless policy explicitly transitions the device to restricted state.

## Related SDR

`SDR-LIC-004` through `SDR-LIC-011`