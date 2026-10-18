# Licensing Architecture

Licensing separates commercial ownership from runtime execution. A device is not authorized because it is registered, because a customer paid, or because a package is installed; it is authorized only when the required signed grant and runtime conditions are valid.

## Core model

~~~mermaid
flowchart LR
    E[Customer Entitlement] --> A[Allocation]
    A --> G[Device-bound Signed Grant]
    G --> V[Local Verification]
    V --> C[Dependency / Time / Capacity Checks]
    C --> R[Runtime Permission]
~~~

## Domain responsibilities

| Concept | Meaning | System of record |
|---|---|---|
| Entitlement | What the customer commercially owns | LMS commercial state |
| Allocation | How pooled rights are distributed | LMS licensing state |
| Grant | Signed executable authorization | LMS issued artifact + edge accepted state |
| Effective runtime right | What the device may execute now | Edge License Agent |

## Required distinctions

- registration != licensing
- licensing != capacity
- payment/renewal approval != accepted device authorization
- marketplace purchase/trial request != executable permission
- installed package != licensed feature

## Supported commercial forms

- subscription base
- perpetual base
- co-terminating subscription add-on
- explicitly independent add-on
- perpetual base with subscription add-on
- policy-configurable trial
- pooled quantities reallocated between devices/sites

## Lifecycle invariants

1. Active allocations never exceed purchased/approved entitlement quantity.
2. Replacement grants supersede prior revisions; old/new rights cannot remain indefinitely additive.
3. Commercial expiry, offline freshness and grace remain separate clocks.
4. Check-in never extends paid commercial expiry.
5. Offline renewal becomes active only after local receipt and acceptance.
6. Dependent add-ons become dormant when their required base is inactive unless explicitly independent.

## Security model

Grants are device-bound, digitally signed and verified locally. Devices persist anti-rollback state and reject stale revisions. Signing private keys remain in the protected signing boundary.

## Failure behavior

Central LMS outage does not immediately invalidate a still-valid offline grant. Invalid signature, wrong device binding, expired term, stale revision or violated dependency fails authorization according to policy. Recovery/diagnostics remain available where safe.

## Related SDR

`SDR-LIC-*`, `SDR-TRL-*`, `SDR-LIF-*`