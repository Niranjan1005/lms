# ADR-018 — Same Core LMS Codebase for SaaS and Customer-Hosted

**Status:** Approved  
**Decision class:** Product / Deployment Architecture

## Context

The platform must support vendor-operated SaaS and customer-hosted/on-prem deployments. Forking the product would multiply security, release, migration and support cost.

## Decision

SaaS and customer-hosted deployments SHALL use the same core LMS application/domain codebase. Differences SHALL be supplied through configuration and provider adapters for identity, artifact storage, signing, email, telemetry and infrastructure topology.

## Alternatives considered

### Separate SaaS and on-prem forks
Rejected because feature/security fixes would diverge and double release/QA effort.

### SaaS-only control plane with mandatory cloud dependency
Rejected because customer-hosted/air-gapped requirements prohibit mandatory vendor connectivity.

## Consequences

- shared domain behavior and test suites
- deployment providers must have clear interfaces
- customer-hosted packaging must avoid assumptions about cloud services
- HA topology may differ without changing business/domain semantics

## Related requirements

`SDR-PLT-002`, `SDR-PLT-006`, `SDR-PLT-007`