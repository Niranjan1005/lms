# ADR-004 — Traditional Signed Edge Release Packages

**Status:** Approved  
**Decision class:** Edge / Release Architecture

## Context

Target deployments include Linux edge devices today and future Windows-compatible environments. Some customer sites are offline/air-gapped. Requiring Docker/container runtime on every edge host would constrain supported environments and add operational dependencies.

## Decision

Edge application delivery SHALL use manifest-driven traditional signed release packages rather than making Docker a platform dependency.

Packages include signed metadata plus application/UI/dependency/config/migration/install/rollback/health artifacts. Linux handlers are implemented first; interfaces remain compatible with future Windows-native handlers.

Models remain independently versioned/encrypted artifacts and may be coordinated through a Release Set.

## Alternatives considered

### Docker-only edge deployment
Rejected because it would narrow target environments and complicate some customer-hosted/Windows/offline use cases.

### Manual file-copy installers
Rejected because they do not provide deterministic verification, migration, health and rollback semantics.

## Consequences

### Positive
- works in constrained/offline environments
- no container runtime dependency
- package can carry deterministic migration/health/rollback logic
- future Windows packaging remains feasible

### Negative / risk
- installer/update manager must handle OS differences explicitly
- package format/security is more responsibility for LMS/edge team
- script execution must be tightly constrained

## Related requirements

`SDR-PLT-004`, `SDR-PLT-005`, `SDR-OTA-006` through `SDR-OTA-010`

## Follow-up

ADR-010 freezes the exact archive/handler format before Update Manager implementation freeze.