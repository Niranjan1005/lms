# Dynamic License Policy Model

The license system must avoid feature-specific columns such as `ppe_enabled`. Rights are represented by generic grants, constraints and dependencies.

## Grant model

A grant contains:
- subject scope: customer/product/device/site
- capability code
- grant type: base/add-on/trial/perpetual/subscription
- quantity/limit constraints
- valid-from / valid-until
- offline/grace policy
- revision and supersession
- dependencies
- update-right policy
- signature metadata

## Constraint examples

~~~json
[
  {"key": "camera_count", "op": "lte", "value": 8},
  {"key": "site_id", "op": "in", "value": ["site_a", "site_b"]},
  {"key": "model_family", "op": "in", "value": ["ppe_v7"]}
]
~~~

## Update-right policy

Preferred explicit schema:

~~~json
{
  "mode": "remaining_major_updates",
  "remaining_updates": 1,
  "until_version": null
}
~~~

Supported modes may include `unlimited`, `during_active_term`, `remaining_major_updates`, `until_version`, and `none`.

## Dependency semantics

Dependent add-ons become dormant when required base grants are not active unless explicitly marked independent by policy.