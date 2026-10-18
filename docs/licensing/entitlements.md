# Entitlements & Allocations

Example entitlement: PPE = 40 camera rights.

~~~text
Device A = 16
Device B = 12
Device C = 8
Unallocated = 4
~~~

The customer/admin may redistribute rights without a new purchase while total allocation stays within the purchased pool.

## Reallocation controls

1. Validate total allocation.
2. Calculate affected device grants.
3. Issue superseding revisions.
4. Prevent temporary double-allocation beyond approved transition policy.
5. Synchronize online or through offline package.
6. Audit before/after values and actor.

## Customer, device and site scope

A device is commercially owned by one customer but may serve multiple sites through explicit device-site assignments.

A device-bound grant may contain site-specific limits. Example:

~~~json
{
  "device_id": "dev_x",
  "capability": "ppe_detection",
  "site_limits": [
    {"site_id": "site_a", "max_cameras": 4},
    {"site_id": "site_b", "max_cameras": 8}
  ]
}
~~~

The grant remains bound to the device, while constraints may partition the permitted quantity by site.

## Allocation invariant

For every entitlement item:

~~~text
sum(active allocations) <= purchased/approved entitlement quantity
~~~

Reallocation must preserve this invariant transactionally and must not rely on UI-only validation.
