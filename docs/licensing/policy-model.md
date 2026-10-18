# Dynamic License Policy Model

The licensing model is generic and data-driven. New features/products should normally be onboarded through catalog/policy/constraint metadata rather than adding feature-specific schema columns or hard-coded licensing branches.

## Grant policy inputs

Effective grant policy is derived from:
- product/feature catalog definition
- customer entitlement item
- allocation
- term type and dates
- product/customer/site/device policy hierarchy
- trial/campaign rules
- base/add-on dependencies
- update-right policy
- approved exceptions/overrides

## Generic grant shape

A grant contains:
- subject: customer/product/device and optional site constraints
- capability code
- grant type: base/add-on/trial/subscription/perpetual
- constraints
- commercial validity
- offline/grace policy
- revision/supersession
- dependencies
- update-right policy
- policy/source revisions
- signature metadata

## Constraint model

~~~json
[
  {"key": "camera_count", "op": "lte", "value": 8},
  {"key": "site_id", "op": "in", "value": ["site_a", "site_b"]},
  {"key": "model_family", "op": "in", "value": ["ppe_v7"]}
]
~~~

Supported operators/types are allowlisted/versioned. Unknown security-critical constraint operators are rejected rather than ignored.

## Constraint resolution

Constraints from entitlement/allocation/policy are combined conservatively: lower-scope configuration cannot expand commercial quantity beyond the entitlement/allocation; security minima cannot be relaxed by ordinary policy override.

## Dependencies

A capability may require base capabilities/grants. Dependency state is evaluated at runtime; a dependent add-on becomes dormant when required base authorization is inactive unless product policy explicitly marks it independent.

## Update rights

~~~json
{
  "mode": "remaining_major_updates",
  "remaining_updates": 1,
  "until_version": null
}
~~~

Supported modes include `unlimited`, `during_active_term`, `remaining_major_updates`, `until_version`, and `none`. Update Manager checks update rights separately from feature execution rights.

## Trials

Trial policy adds eligibility, activation-start behavior and duration but still produces a normal signed time-limited grant. Trial state is not a special UI-only boolean.

## Policy snapshot/audit

Grant issuance records the relevant resolved policy/source revisions so support can explain why a grant was produced. Sensitive override source/approval is auditable.

## Extensibility rule

Adding a new feature quantity type should require a registered constraint schema/validator and runtime enforcement support; it should not require new `feature_x_enabled` DB columns.

## Related SDR

`SDR-LIC-005`, `SDR-LIC-006`, `SDR-LIC-010`, `SDR-TRL-*`