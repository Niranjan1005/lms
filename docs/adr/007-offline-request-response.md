# ADR-007 — Signed Offline Request/Response

**Status:** Approved

## Decision

Offline/air-gapped workflows use device-bound signed requests and centrally issued signed response packages linked by request ID and nonce. Relay devices are transport-only.

## Consequences

The same trust model works online and offline while limiting replay and preventing relay workstations from becoming signing authorities.