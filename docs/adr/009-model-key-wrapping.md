# ADR-009 — Model Encryption and Key Wrapping

**Status:** Open Security Decision  
**Decision class:** Security / Model Protection

## Context

Model artifacts are valuable IP and must be distributable through online/offline routes without embedding a universal password. Authorization must tie model use to a valid entitlement/device or deployment context.

## Baseline already approved

- model artifacts are encrypted and signed
- random content-encryption keys are preferred per artifact/release
- entitlement controls permission to use a model
- device/deployment identity controls authorized unwrap/use
- plaintext content keys are not stored in normal LMS DB/logs
- a universal customer-wide/static model password is prohibited

## Options to decide

### Per-device wrapped DEK
Strong device binding and revocation granularity; larger metadata/packaging overhead.

### Per-deployment/site wrapped DEK
Lower wrapping overhead; broader compromise scope.

### Online KMS-assisted unwrap only
Strong central control but incompatible with fully air-gapped operation unless offline escrow/derived mechanism exists.

### Local platform secure storage
TPM/secure element/OS key store where available, with fallback profile needed for heterogeneous devices.

## Required decision output

The final ADR amendment/superseding ADR must freeze envelope-encryption algorithm/profile, KEK hierarchy, KMS/HSM integration, wrapping scope, local protected storage, rotation/recovery and offline package behavior.

## Security considerations

Root/administrator compromise may expose plaintext model memory during legitimate execution; encryption protects storage/distribution and raises misuse cost but does not create impossible software-only DRM guarantees.

## Decision deadline

Before production Model OTA implementation/security freeze.

## Related requirements

`SDR-MOD-002`, `SDR-MOD-004`, `SDR-MOD-005`