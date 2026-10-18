# License Agent

The License Agent is the local policy-enforcement authority for licensed runtime features. It validates signed central authorization and exposes an explicit local authorization contract to analytics services.

## Responsibilities

- load and verify signed grants
- validate trusted key ID/algorithm/canonicalization profile
- enforce device/product/site binding
- enforce commercial valid-from/valid-until
- enforce offline freshness and grace independently
- enforce revision/supersession/anti-rollback
- resolve base/add-on dependencies
- enforce quantity and dynamic constraints
- use persisted last-known trusted time
- expose effective feature state/reason codes
- produce signed acceptance/check-in evidence where required

## Startup

On service startup:
1. load protected local identity/trust state
2. validate persisted grant artifacts
3. reject rollback to a lower accepted revision
4. evaluate trusted-time state
5. publish effective authorization state
6. keep protected analytics disabled until authorization is established

## Authorization response

~~~json
{
  "feature_id": "ppe_detection",
  "decision": "allow",
  "grant_id": "grant_1001",
  "revision": 8,
  "effective_limits": {"camera_count": 4},
  "commercial_valid_until": "2027-10-31T23:59:59Z",
  "offline_fresh_until": "2026-10-25T12:00:00Z",
  "reason_codes": []
}
~~~

Possible decisions are `allow`, `restricted`, and `deny`. Reasons are machine-readable and safe for support.

## Runtime enforcement

Analytics services ask the License Agent at actual workload creation/change boundaries. A cached allow decision is bounded by grant/time/revision context and must be invalidated when grant/policy state changes.

## Failure behavior

Invalid signature, wrong subject, revoked trust key, stale rollback revision or malformed signed payload fail closed. Central LMS unavailability alone does not immediately fail a still-valid offline grant.

## Recovery accessibility

When license execution is denied, the device should retain access to license import, diagnostics, support status and recovery workflows where product safety allows.