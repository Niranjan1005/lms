# Device Transfer, Replacement, Rehost & Revocation

## Transfer between customer/site ownership contexts

1. Create transfer request with current owner/site, requested owner/site, reason and effective intent.
2. Validate caller authority and affected entitlements/allocations.
3. Require approval according to policy; cross-customer transfer is always sensitive.
4. Freeze or supersede grants that would become invalid under the new ownership.
5. Update ownership/site assignments only after approval.
6. Issue new grants under the valid target entitlement context.
7. Reconcile old allocations and audit before/after ownership.

Silent overwrite of owner/site is prohibited.

## Replacement device

For device replacement:
- register replacement identity as a new device
- approve replacement/rehost relationship
- return or reassign allocation from retired device
- issue new device-bound grant
- retire old device/grant binding
- preserve audit lineage between old and replacement devices

## Rehost

Rehost is used when the physical system is intended to remain the same commercial installation but cryptographic/major hardware identity changed. Major motherboard/key changes enter `REHOST_REQUIRED` until approved.

## Revocation

Connected device: central revocation/superseding state is delivered at next sync/check-in according to policy.

Air-gapped device: immediate remote revocation is impossible. Revocation becomes effective after importing signed updated state or when current offline authorization expires.

## Diagnostics in grace/restricted state

Where product safety permits, grace/restricted mode should preserve access to diagnostics, license recovery/import, support status and existing customer data. Expired commercial rights should disable unauthorized analytics execution, not make recovery impossible.