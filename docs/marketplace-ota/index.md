# Marketplace & OTA Architecture

Marketplace and OTA are different responsibilities inside one LMS. Marketplace determines what may be discovered/requested; OTA determines how approved compatible content is safely delivered and activated.

## Capability split

| Marketplace | OTA |
|---|---|
| feature discovery | release/model resolution |
| eligibility/trial/purchase request | deployment target selection |
| commercial/catalog metadata | download/offline bundle generation |
| entitlement/capacity preview | signature/hash verification |
| request/approval status | install/health/rollback |

Neither side alone authorizes runtime execution. Final activation requires valid grant + compatibility + installed healthy content + local capacity approval.

## End-to-end flow

~~~mermaid
flowchart LR
    A[Discover Feature] --> B[Compatibility / Capacity Preview]
    B --> C[Trial or Purchase Request]
    C --> D[Commercial / Policy Approval]
    D --> E[Signed Grant]
    E --> F[Resolve Release Set]
    F --> G[Online or Offline Delivery]
    G --> H[Verify + Stage]
    H --> I[Local Capacity + Health]
    I --> J[Commit / Rollback]
    J --> K[Runtime Enable + Receipt]
~~~

## Release principles

- Stable is default for automatic production deployment
- LTS is explicitly designated
- published artifacts/manifests are immutable
- application and models are independently versioned
- coherent Release Set governs compatibility and rollback
- delta/minimal transfer avoids re-downloading verified local content
- offline and online use the same artifact trust model

## Failure semantics

Purchase success does not imply installation. Download success does not imply activation. Install without health success does not become Active. Failed deployment preserves/returns to known-good release state.

## Related SDR

`SDR-MKT-*`, `SDR-OTA-*`, `SDR-MOD-*`