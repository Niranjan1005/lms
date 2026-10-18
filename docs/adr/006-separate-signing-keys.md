# ADR-006 — Separate License and Release Signing Keys

**Status:** Approved  
**Decision class:** Security / Cryptographic Architecture

## Context

License grants and software/model releases represent different trust purposes. Reusing one signing key would increase blast radius and make rotation/incident handling ambiguous.

## Decision

Use separate cryptographic key purposes and key identities for license/grant signing and software/model release signing. Additional separation for model/key-wrapping operations MAY be introduced without changing this ADR.

## Alternatives considered

### One platform-wide signing key
Rejected because compromise, rotation and authorization policy would affect unrelated trust domains.

### Application-stored private keys
Rejected because normal application/database compromise would become signing compromise.

## Consequences

- reduced compromise blast radius
- independent rotation/recovery windows
- distinct authorization policy for signing requests
- devices must trust/version multiple public-key purposes
- audit records must include key purpose and key ID

## Security / operational impact

Production private keys remain in KMS/HSM/equivalent protected provider. Trust-store distribution must support overlap between active and retiring verification keys.

## Related requirements

`SDR-SEC-003`, `SDR-SEC-004`, `SDR-MOD-002`