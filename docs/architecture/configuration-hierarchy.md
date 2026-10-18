# Configuration & Policy Hierarchy

The platform must resolve configuration deterministically across platform, product, customer, site and device scopes.

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

Only explicitly allowed policy keys may be overridden at lower scopes. Security minimums may be marked non-relaxable.

## Policy domains

- offline authorization duration
- grace duration
- trial duration and eligibility
- release channel eligibility
- automatic/manual OTA mode
- maintenance window
- rollback behavior
- model-only update permission
- concurrency limits
- notification preferences
- audit retention
- capacity override policy

## Example resolved policy

~~~json
{
  "offline_days": 7,
  "grace_days": 7,
  "trial_days": 14,
  "ota_mode": "auto",
  "release_channel": "stable",
  "maintenance_window": {"start": "01:00", "end": "03:00", "timezone": "site"},
  "auto_rollback": true,
  "model_only_updates": true
}
~~~

## Governance

Every resolved policy response should include source metadata so operators can see which scope supplied each effective value. Changes to sensitive policy keys are audited.