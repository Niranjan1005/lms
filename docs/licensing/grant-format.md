# Signed Grant Canonical Format

The signed grant is a device-verifiable authorization artifact. The final binary/serialization format is implementation-specific, but signing semantics must be deterministic.

## Canonical payload example

~~~json
{
  "schema_version": 1,
  "grant_id": "grant_001",
  "revision": 8,
  "supersedes": "grant_000",
  "issued_at": "2026-10-18T12:00:00Z",
  "subject": {
    "customer_id": "cust_001",
    "product_id": "analytics",
    "device_id": "dev_001"
  },
  "capabilities": [
    {
      "code": "ppe_detection",
      "limits": [{"key": "camera_count", "op": "lte", "value": 4}],
      "dependencies": [{"capability": "analytics_base", "required": true}]
    }
  ],
  "commercial": {"type": "subscription", "valid_until": "2027-10-31T23:59:59Z"},
  "runtime": {"offline_days": 7, "grace_days": 7},
  "key_id": "lic_sign_01"
}
~~~

## Signing requirements

1. Remove the signature field from the payload.
2. Normalize field order/encoding using a documented canonicalization method.
3. Hash/sign the canonical bytes using the active license-signing key.
4. Attach `key_id`, algorithm and signature.
5. Device reconstructs the same canonical bytes before verification.

## Anti-rollback

Device persists the highest accepted revision/sequence per relevant grant lineage and rejects older revisions unless an explicit signed recovery mechanism exists.

## Key rotation

Verification trust store may contain current and retiring public keys. New grants use only the active key; older valid grants remain verifiable during the planned rotation window.