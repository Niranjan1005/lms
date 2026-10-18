# ADR-007 — Signed Offline Request/Response Protocol

**Status:** Approved  
**Decision class:** Offline / Security Architecture

## Context

Air-gapped devices cannot rely on live API calls. Offline media/relay workstations cannot be trusted with authority to create licenses or release packages.

## Decision

Offline/air-gapped workflows SHALL use device-signed requests and centrally issued signed response packages bound to request ID, nonce and device identity.

Relay/media components SHALL remain transport-only and SHALL NOT contain signing private keys or authority to alter entitlement/grant state.

## Protocol properties

- request includes request ID, nonce, device identity reference, current grant/release/model inventory and requested operation
- central verifies device signature, ownership, request freshness and replay state
- response is bound to request ID/nonce/device
- edge verifies signature/hash/binding/revision before use
- accepted activation/install emits signed receipt for later reconciliation

## Alternatives considered

### USB license file with no request binding
Rejected because replay/cross-device reuse is harder to prevent.

### Signing on relay workstation
Rejected because it turns a portable endpoint into a high-value authority and breaks central commercial governance.

## Consequences

- offline behavior preserves the same trust semantics as online issuance
- replay/cross-device misuse is bounded
- fully air-gapped revocation remains delayed until signed import or authorization expiry
- field operators need deterministic package/error handling

## Related requirements

`SDR-OFF-001` through `SDR-OFF-009`