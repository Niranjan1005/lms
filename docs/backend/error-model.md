# Error Model

Errors are stable machine-readable contracts for clients, edge agents, support and automation. They must be actionable without exposing internal stack traces or sensitive tenant/security data.

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
| Category | Typical HTTP | Meaning |
|---|---:|---|
| validation | 400/422 | malformed/invalid request or invariant |
| authentication | 401 | caller identity not accepted |
| authorization | 403 | authenticated but not permitted |
| not_found | 404 | object unavailable in caller scope |
| conflict | 409 | concurrent/stale/duplicate/business state conflict |
| rate_limit | 429 | abuse/backpressure policy |
| dependency | 424 | required base/model/runtime/state unavailable |
| temporary | 503 | retryable platform/dependency outage |

## Error-code structure

Baseline format:
~~~text
LMS-<DOMAIN>-<HTTP>-<NNN>
~~~

Domain and code meaning are stable. A code is never repurposed to mean a different failure.

## Retry semantics

`retryable=true` is based on workflow behavior, not simply HTTP 5xx. Examples: signing provider unavailable may be retryable; invalid signature is not; optimistic-concurrency conflict may require caller refresh rather than blind retry.

## Security-safe errors

Authentication and cross-tenant errors may deliberately avoid confirming account/object existence. Full internal reason is recorded in secure logs/audit with request ID where appropriate.

## Validation details

Details may include field/revision/reason-code data safe for the caller. They SHALL NOT include SQL, stack trace, filesystem path, secret/token, private key, another tenant's identifiers or decrypted model data.

## Offline/edge errors

Offline/import/update errors need deterministic reason codes that field operators can map to action: wrong device/request, replay/stale revision, unknown signing key, invalid signature/hash, unsupported source version, insufficient disk, dependency mismatch, capacity failure, health/rollback failure.

## Background jobs

Durable jobs store final error code/category/retry metadata separately from transient stack/debug detail so operations can safely inspect and reprocess approved failures.

## Correlation

Every client-visible error carries request ID. Deployment/job/receipt errors also carry their workflow identifiers for end-to-end support correlation.

## Catalogue governance

New codes are added to Support Error Code Catalogue with customer-safe message and operator action. Removed behavior leaves old code reserved rather than reused.