# Critical Flow Test Matrix

| Flow | Happy path | Negative/security cases | Offline case | Rollback/recovery |
|---|---|---|---|---|
| Device enrollment | new valid device registers | reused token, forged key, duplicate identity | assisted registration package where supported | retry without duplicate device |
| Base activation | entitled device receives grant | wrong device, expired term, stale revision | signed response import | preserve previous valid grant |
| Reallocation | pool rebalanced within quantity | concurrent edit, over-allocation | affected devices receive new grants later | no indefinite double-use |
| Trial | eligible trial activates | second trial, expired campaign | offline trial grant | expiry/convert behavior |
| Renewal | new term accepted | payment not approved, stale package | offline renewal import | old grant until expiry/policy |
| Capacity | feasible workload passes | unsupported GPU/runtime, stale inventory | local authoritative assessment | recommendation, no rights loss |
| App OTA | Stable update succeeds | bad hash, dependency missing | offline package import | coherent release-set rollback |
| Model OTA | missing model downloaded | unauthorized decryption, hash mismatch | encrypted model import | restore previous model |
| Rehost | approved replacement identity | spoofed change, unauthorized approver | offline device receives new binding later | old identity retired |
| Revocation | online device receives revoke | replayed old grant | air-gapped device ages out/imports revoke | diagnostics remain available |
| Clock rollback | normal trusted time moves forward | backward jump | no central connectivity | restrict/revalidate per policy |
| ERP sync | approved line creates/updates entitlement | duplicate/out-of-order/unknown SKU | n/a | reconciliation surfaces mismatch |

## Minimum automation expectation

Critical-path API and edge verification tests run in CI. Upgrade/rollback, offline bundle, migration and hardware-capacity scenarios run in dedicated integration/system environments with representative fixtures.