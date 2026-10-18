# Release Manifest Schema

The release manifest is the machine-readable contract between Release Management and the edge Update Manager. It is signed and immutable after publication.

## Example

~~~json
{
  "manifest_version": 1,
  "release_id": "rel_ppe_4_2_1",
  "feature_id": "ppe_detection",
  "version": "4.2.1",
  "channel": "stable",
  "platforms": [
    {"os": "ubuntu", "versions": ["22.04", "24.04"], "arch": ["x86_64", "aarch64"]}
  ],
  "requirements": {
    "runtime": ">=3.7 <4.0",
    "disk_free_mb": 2500,
    "ram_mb": 8192
  },
  "artifacts": [
    {
      "artifact_id": "art_app_421",
      "type": "application",
      "version": "4.2.1",
      "sha256": "...",
      "size": 123456789
    }
  ],
  "models": [
    {"model_id": "ppe_detector", "version_range": ">=7.3 <8.0", "required": true}
  ],
  "migrations": {
    "config_schema_from": [4,5],
    "config_schema_to": 6,
    "automatic": true
  },
  "health_checks": [
    {"type": "http", "target": "http://127.0.0.1:9000/health", "timeout_sec": 30}
  ],
  "rollback": {"supported": true, "minimum_free_mb": 3000},
  "signature": {"key_id": "release_sign_01", "algorithm": "Ed25519", "value": "..."}
}
~~~

## Rules

- Manifest canonicalization is defined before signing.
- Artifact hash is mandatory.
- Dependencies use explicit version ranges.
- Installation scripts are treated as signed artifacts, never unsigned inline commands.
- A published manifest is immutable; corrections create a new release/version.
- Device must reject unsupported manifest versions.