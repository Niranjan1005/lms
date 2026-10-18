# ADR-005 — Device-Generated Cryptographic Identity

**Status:** Approved

## Decision

Each device generates/holds an asymmetric key pair and registers the public key with LMS. Hardware fingerprint is supporting/versioned identity evidence; MAC address is never the sole device identity.

## Consequences

Enrollment and grants can bind to cryptographic identity. Major identity change requires controlled rehost rather than silent rebinding.