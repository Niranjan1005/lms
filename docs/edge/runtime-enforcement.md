# Runtime Enforcement & Protected Local State

License enforcement must occur at the actual service/runtime boundary, not only in portal/UI controls.

## Authorization decision

Before starting or expanding a protected feature, the runtime adapter checks:
1. signed grant validity
2. device/product/site scope
3. grant revision/supersession
4. commercial term
5. offline freshness/grace
6. feature dependencies
7. requested quantity/limits
8. installed release/model compatibility
9. local capacity result
10. runtime health

## Fail-closed vs recoverability

Unauthorized analytics execution fails closed. Recovery functions such as license import, diagnostics and support status should remain accessible where product safety permits.

## Protected local state

Persist at minimum:
- device private-key reference/protected key handle
- highest accepted grant revision/sequence
- last-known trusted time
- current grant set
- current and previous known-good release set
- installed model inventory
- pending signed receipts
- latest local capacity assessment/workload hash

State that prevents rollback/replay should use the strongest practical local protection available for the platform.

## Clock handling

A suspicious backward clock jump does not automatically extend rights. The License Agent uses persisted trusted-time evidence and moves to revalidation/restricted behavior according to policy.

## Runtime quantity enforcement

Camera/feature limits are checked when workloads are created/changed, not only at startup. A device serving multiple sites enforces both total device limits and applicable site constraints.

## Service restart

After restart, the runtime reconstructs effective authorization from verified persisted grants and protected monotonic state before enabling protected analytics.