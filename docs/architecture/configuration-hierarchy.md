# Configuration & Policy Hierarchy

The platform resolves policy deterministically across platform, product, customer/entitlement, site and device scopes. Lower-level overrides are allowed only for explicitly overrideable keys and can never weaken non-relaxable security controls.

## Resolution order

~~~text
Platform Default
    ↓
Product Override
    ↓
Customer / Entitlement Override
    ↓
Site Override
    ↓
Device Override
~~~

For a key not specified at a lower scope, the nearest higher-scope value is inherited.

## Policy metadata

Every policy key should define:
- key/name
- data type/unit
- default value
- allowed scope(s)
- min/max/enum constraints
- whether lower scopes may override
- whether stricter-only override is required
- whether maker-checker is required
- effective-from/expiry where relevant

## Policy domains

- offline authorization duration
- grace duration
- trial duration and eligibility
- release channel eligibility
- AUTO/MANUAL OTA
- maintenance window
- rollout concurrency/batch size
- rollback behavior
- model-only update permission
- notification preferences
- audit retention
- capacity warning/override policy
- telemetry delivery/retention policy when approved

## Example resolved policy

~~~json
{
  "offline_days": 7,
  "grace_days": 7,
  "trial_days": 7,
  "ota_mode": "auto",
  "release_channel": "stable",
  "maintenance_window": {"start": "01:00", "end": "03:00", "timezone": "site"},
  "auto_rollback": true,
  "model_only_updates": true
}
~~~

The 7-day trial shown above is the platform default. A customer/product campaign may resolve another value only through an allowed, auditable override.

## Resolved-policy response

Operators need to know not only the effective value but where it came from. Resolved policy should expose source scope, source object ID/revision and whether the value is inherited/overridden.

## Conflict rules

- invalid lower-scope values are rejected, not silently clamped
- expired overrides fall back to inherited policy
- non-relaxable security minima cannot be overridden
- an approval-bound override is invalid if the target revision/payload changes
- device-specific exception must not mutate customer-wide policy

## Change/audit

Sensitive policy changes generate audit events with previous/effective value, source scope, actor/reason and approval reference. Policy revision is included in downstream grant/deployment evidence where behavior depends on it.

## Related SDR

`SDR-TRL-001`, `SDR-LIF-002`, `SDR-LIF-003`, `SDR-OTA-004`, `SDR-OTA-005`, `SDR-SEC-008`