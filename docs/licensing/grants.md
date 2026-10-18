# Device-Bound Grants

A grant is the signed executable permission derived from entitlement, allocation and policy.

~~~json
{
  "grant_id": "grant_1001",
  "device_id": "dev_310",
  "capabilities": [{
    "feature": "ppe_detection",
    "limit": {"type": "camera_count", "value": 4}
  }],
  "runtime_policy": {"offline_days": 7, "grace_days": 7},
  "revision": 2,
  "supersedes_grant_id": "grant_0988",
  "signature": "..."
}
~~~

Supersession is mandatory for replacement grants to prevent accidental aggregation.

Perpetual licenses may carry explicit update policies such as unlimited, N future major updates, or until-version.