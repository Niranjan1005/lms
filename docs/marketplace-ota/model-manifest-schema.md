# Model Manifest Schema

Model manifests are independent from application releases so compatible model-only OTA does not force application redownload. The manifest is signed and immutable after publication.

## Canonical fields
~~~json
{
  "manifest_version": 1,
  "model_release_id": "mr_ppe_7_3_0",
  "model_id": "ppe_detector",
  "version": "7.3.0",
  "channel": "stable",
  "framework": "TensorRT",
  "precision": "FP16",
  "input": {"width": 640, "height": 640, "layout": "NCHW"},
  "compatibility": {
    "products": ["ai_box"],
    "architectures": ["x86_64"],
    "gpu_families": ["nvidia"],
    "runtime": ">=3.7 <4.0",
    "feature_release": ">=4.2 <5.0",
    "config_schema": ">=6"
  },
  "artifact": {
    "uri_ref": "artifact://models/ppe/7.3.0",
    "sha256": "...",
    "encrypted": true,
    "encryption_profile": "model-envelope-v1",
    "size": 901234567
  },
  "validation": {
    "warmup_required": true,
    "expected_output_schema": 3,
    "health_profile": "ppe-default-v2"
  },
  "key_delivery": {
    "wrapping_profile": "pending-adr-009"
  },
  "signature": {"key_id": "release_sign_01", "algorithm": "Ed25519", "value": "..."}
}
~~~

## Required semantics

- `manifest_version` controls schema compatibility
- `model_release_id` is immutable identity
- version/channel are metadata, not trust proof
- compatibility is evaluated before download/activation
- artifact URI is a repository reference; hash/signature establish integrity
- encrypted=true is required for protected production model artifacts according to policy
- validation describes minimum warm-up/health expectations
- signature covers canonical manifest excluding signature value according to release signing format

## Key handling

Repository stores encrypted model material. Entitlement/grant controls permission to use the model; authorized key wrapping/unwrapping controls access to the content key. A universal embedded password is prohibited.

## Publication

Manifest/artifact bytes become immutable once Published. Correction creates a new model release/version. Promotion changes channel eligibility, not manifest content, unless the design explicitly models channel as separate mutable release metadata.

## Local validation

Edge checks schema version, trusted signing key, signature, hash, target product/architecture/runtime/feature compatibility, available disk, grant rights and local capacity before activation.

## Inventory/delta

Device inventory reports model ID/version/hash/status. Central bundle builder skips transfer only when local content identity/hash satisfies the required manifest.

## Related SDR

`SDR-MOD-001` through `SDR-MOD-007`