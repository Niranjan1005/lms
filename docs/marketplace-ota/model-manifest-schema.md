# Model Manifest Schema

Model metadata is independent from application releases so compatible model-only OTA does not force application redownload.

## Example

~~~json
{
  "manifest_version": 1,
  "model_release_id": "mr_ppe_7_3_0",
  "model_id": "ppe_detector",
  "version": "7.3.0",
  "channel": "stable",
  "framework": "TensorRT",
  "precision": "FP16",
  "input": {"width": 640, "height": 640},
  "compatibility": {
    "architectures": ["x86_64"],
    "gpu_families": ["nvidia"],
    "runtime": ">=3.7 <4.0",
    "feature_release": ">=4.2 <5.0"
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
    "expected_output_schema": 3
  },
  "signature": {"key_id": "release_sign_01", "algorithm": "Ed25519", "value": "..."}
}
~~~

## Key handling principle

The repository stores encrypted model material. Entitlement controls permission to use the model; device authorization controls decryption. A universal embedded model password is prohibited.