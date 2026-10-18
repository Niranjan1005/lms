# ADR-003 — Marketplace and OTA Remain Inside LMS

**Status:** Approved  
**Decision class:** Product / Platform Architecture

## Context

Feature discovery, trial/purchase eligibility, compatibility, capacity preview, release selection and deployment all depend on the same customer, device, entitlement, policy, capacity and audit data.

## Decision

Marketplace and OTA SHALL be distinct logical modules within LMS rather than separate standalone products in the initial architecture.

Artifact storage may use an external repository, and delivery infrastructure may later be extracted, but business eligibility and orchestration remain governed by LMS.

## Alternatives considered

### Separate Marketplace service/application
Rejected initially because it would duplicate customer/device/entitlement state and create synchronization complexity.

### Separate OTA control plane
Rejected initially because release eligibility, update rights and device lifecycle already live in LMS.

## Consequences

### Positive
- one source of truth for eligibility and device state
- easier trial/purchase-to-deployment flow
- common audit and authorization model
- reduced duplicated integration logic

### Negative / risk
- LMS has broader scope
- strong internal module boundaries are required
- scaling of artifact transfer must remain separated from transactional API concerns

## Related requirements

`SDR-MKT-001` through `SDR-MKT-005`, `SDR-OTA-*`