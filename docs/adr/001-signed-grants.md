# ADR-001 — Digitally Signed Device-Bound Grants

**Status:** Approved  
**Decision class:** Security / Licensing  
**Scope:** Central LMS + Edge License Agent

## Context

LMS must authorize feature execution on connected, intermittently connected and fully air-gapped devices. A central database lookup alone cannot authorize offline runtime, and reusable license files would be vulnerable to copying between devices.

## Decision

Use centrally issued, digitally signed, device-bound grants as the executable authorization artifact.

A grant SHALL include subject identity, capability/limits, commercial validity, offline/grace policy, revision/supersession, dependencies and signing metadata. The device verifies the grant using a trusted public key before runtime use.

Production signing private keys remain outside normal LMS application/database storage.

## Alternatives considered

### Central online lookup only
Rejected because air-gapped/offline operation is a first-class requirement.

### Unsigned local license files
Rejected because tampering cannot be reliably detected.

### Customer-wide reusable license key/file
Rejected because it increases cloning/reuse risk and weakens device-level allocation/revocation.

## Consequences

### Positive
- offline verification works without central connectivity
- tampering/forgery is detectable
- device-specific quantities and dependencies can be enforced
- supersession/revision supports controlled renewal/reallocation

### Negative / cost
- key custody, rotation and trust-store management are required
- offline revocation is delayed until import/expiry
- compromised root access on the edge remains outside full software control

## Security / operational impact

- grant verification fails closed
- devices persist highest accepted revision
- signing outage blocks new issuance but not already-valid grants
- support must distinguish issued, delivered and accepted states

## Related requirements

`SDR-LIC-004`, `SDR-LIC-007`, `SDR-LIC-008`, `SDR-SEC-003`, `SDR-SEC-004`

## Follow-up

Grant canonicalization and exact wire format are finalized in implementation/OpenAPI/schema work without changing this decision.