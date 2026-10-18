# ADR-009 — Model Encryption and Key Wrapping

**Status:** Open Security Decision

## Baseline

Model artifacts are encrypted and signed. Entitlement controls authorization and device identity controls whether content-key material may be unwrapped/used.

## Decision required

Finalize envelope-encryption algorithm, key hierarchy, KMS/HSM integration, per-device/per-deployment wrapping strategy, edge secure-storage expectations and rotation/recovery procedure. A universal model password is prohibited.