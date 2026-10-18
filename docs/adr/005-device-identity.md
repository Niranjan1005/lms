# ADR-005 — Device-Generated Cryptographic Identity

**Status:** Approved  
**Decision class:** Security / Device Lifecycle

## Context

MAC address, hostname or a customer-shared activation code can be copied/spoofed and are insufficient for device-bound grants. Hardware can also change legitimately over device lifetime.

## Decision

Each device SHALL generate/hold an asymmetric key pair and register its public key with LMS. A versioned weighted hardware fingerprint is supporting identity evidence; MAC/network identifiers are evidence only.

Minor hardware changes are tolerated according to fingerprint policy. Major identity change, key loss or motherboard-level change enters `REHOST_REQUIRED` and requires controlled approval.

## Alternatives considered

### MAC-address identity
Rejected because MACs are mutable/spoofable and unreliable across replacements.

### Server-generated shared device secret
Rejected because centralized secret distribution increases cloning/custody risk.

### Exact immutable hardware hash
Rejected because legitimate RAM/storage/NIC changes would unnecessarily invalidate devices.

## Consequences

- grants/offline requests can bind to a cryptographic principal
- cloning becomes harder than copying a license file
- key storage quality on the edge matters
- rehost/transfer workflows become explicit business/security processes
- hardware fingerprint algorithm must be versioned and testable

## Related requirements

`SDR-DEV-005` through `SDR-DEV-010`