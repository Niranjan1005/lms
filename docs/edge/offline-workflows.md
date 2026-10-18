# Offline & Air-Gapped Workflows

Offline support is a first-class operating mode. The protocol preserves central commercial authority while allowing an isolated device to verify signed grants/releases locally.

## Supported operations
- trial/feature activation
- renewal
- application/feature/UI update
- model update
- revocation/superseding state import
- installation/activation receipt export

## Request package
Contains schema version, request ID + nonce, created/expiry time, device/key identity, customer/product context, requested operation, current grant revisions, installed Release Set/model/artifact inventory, hardware/workload evidence and a device signature over the canonical request.

## Central request validation
Before generating a response LMS validates:
1. schema/canonical signature
2. registered device/key
3. tenant/customer ownership
4. request expiry/age
5. request ID/nonce replay state
6. entitlement/trial/renewal policy
7. current grant/release state
8. compatibility and capacity advisory inputs
9. operator authorization where manual import is involved

## Response package
May contain original request ID + nonce + target-device binding, signed grant revisions, signed Release Set manifest, only missing artifacts where possible, encrypted model material, import expiration/policy and signed hashes/metadata.

## Local import
~~~mermaid
flowchart TD
    A[Copy to quarantine/staging] --> B[Validate package bounds/type]
    B --> C[Verify manifest signature/hash]
    C --> D[Verify request_id + nonce + device binding]
    D --> E[Reject replay / stale grant or release]
    E --> F[Verify grant/dependencies/compatibility]
    F --> G[Local capacity preflight]
    G --> H[Stage release/model]
    H --> I[Migration / warm-up / health]
    I -->|Pass| J[Commit + activate]
    I -->|Fail| K[Rollback]
    J --> L[Generate signed receipt]
    K --> L
~~~

## Anti-replay
Device persists consumed request/response identifiers and highest accepted grant/release revisions as appropriate. A validly signed old package is not automatically reusable.

## Receipt
Receipt records request ID, device, accepted grant revision, Release Set/model versions, result, health and rollback state. It is signed by the device and later reconciled centrally.

## Issued != accepted
Central response generation does not mark an offline device Active. Central state remains Delivered/Pending until signed receipt/check-in confirms acceptance.

## Delta bundles
Central compares reported inventory and includes only required/missing artifacts when safe. Device re-verifies cached content before reuse.

## Revocation limitation
Immediate remote revocation is impossible for a fully air-gapped device. Revocation becomes enforceable after signed state import or expiry of current offline authorization.

## Operator/media security
Relay/media possession grants no authority. Device/request binding, relay controls and archive-parser security apply to all imports.

## Related SDR/ADR
`SDR-OFF-001` through `SDR-OFF-009`; ADR-007