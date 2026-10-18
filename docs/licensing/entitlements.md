# Entitlements & Allocations

Entitlement is the customer's commercial right. Allocation distributes pooled entitlement to device/site scope. Neither object alone is executable on the edge; device execution uses a signed Grant.

## Entitlement item
An entitlement item records customer/product, feature/capability, quantity type + purchased/approved quantity, commercial term/type, dependency/base context, update-right/commercial policy reference, source order/contract/manual approval and revision/status.

## Pool example
~~~text
PPE entitlement = 40 camera rights

Device A = 16
Device B = 12
Device C = 8
Unallocated = 4
~~~

## Core invariant
For every pooled entitlement item:
~~~text
sum(active allocations) <= approved entitlement quantity
~~~

This invariant is enforced transactionally, not only in the UI.

## Allocation scope
An allocation may target device, site or approved scope according to feature policy. A device is commercially owned by one customer but may serve multiple sites.

## Multi-site device
A device-bound grant may partition allocated quantity by site:
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

Site constraints partition permitted use; they do not make the grant transferable between devices.

## Reallocation workflow
1. read entitlement + active allocations under concurrency control
2. validate proposed total and target ownership
3. calculate affected allocation revisions
4. calculate superseding device grants
5. commit allocation/supersession intent transactionally
6. sign/deliver new grants asynchronously
7. receive acceptance/check-in/receipt
8. audit before/after values and reason

## Transition safety
Reallocation must not create indefinite old+new double-use. Online devices receive superseding grants promptly. Offline devices may retain older still-valid grants only within an explicit transition/offline policy while central state remains pending reconciliation.

## Quantity changes
Increasing the purchased pool requires approved commercial state/maker-checker/ERP import according to policy. Capacity recommendations never rewrite entitlement quantity.

## Decommission/replacement
Retiring a device returns/reconciles eligible allocation before reassignment and issues appropriate supersession/revocation state.

## Audit
Entitlement/allocation events record quantity, previous/new revision, targets, commercial source, requester/approver and reason.

## Related SDR
`SDR-LIC-001` through `SDR-LIC-003`, `SDR-LIC-011`