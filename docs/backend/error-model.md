# Error Model

Errors must be machine-readable, stable and safe to expose. Internal stack traces are never returned to clients.

## Envelope

~~~json
{
  "error": {
    "code": "LMS-GRANT-409-001",
    "message": "Grant revision is older than the active device revision.",
    "category": "conflict",
    "retryable": false,
    "details": {"active_revision": 8, "submitted_revision": 7}
  },
  "meta": {"request_id": "req_..."}
}
~~~

## Categories

| Category | Typical HTTP | Examples |
|---|---:|---|
| validation | 400/422 | malformed scope, invalid quantity |
| authentication | 401 | invalid user/device credential |
| authorization | 403 | cross-tenant access, unapproved override |
| not_found | 404 | device/release does not exist in caller scope |
| conflict | 409 | duplicate allocation, stale revision, rehost required |
| rate_limit | 429 | enrollment or request abuse protection |
| dependency | 424 | required base grant/model/runtime unavailable |
| temporary | 503 | signing gateway/artifact service unavailable |

## Rules

- Error codes are documented and never repurposed.
- `retryable` reflects workflow semantics, not only HTTP class.
- Security-sensitive reasons may be intentionally generalized externally while full detail is written to audit/secure logs.
- Offline import errors must be deterministic enough for field operators to recover without site debugging.