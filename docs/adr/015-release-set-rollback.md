# ADR-015 — Coherent Release Set as Deployment/Rollback Unit

**Status:** Approved  
**Decision class:** Edge / OTA

## Context

Application, plugins/features, UI/runtime, models and configuration schemas can have compatibility dependencies. Rolling back only one component after a failed deployment may leave the product inconsistent.

## Decision

Deployment and rollback SHALL operate on a coherent Release Set representing compatible application, feature/plugin, UI/runtime, model and configuration versions.

At least the immediately previous known-good Release Set SHALL be preserved; 2–3 known-good sets are preferred when storage permits.

## Alternatives considered

### Independent component rollback without coordination
Rejected because dependency mismatches can make rollback unsafe.

### No local rollback retention
Rejected because air-gapped/failed central connectivity needs autonomous recovery.

## Consequences

- deterministic health/rollback behavior
- storage reservation required
- manifests need cross-component compatibility metadata
- model-only updates still participate in release-set compatibility state

## Related requirements

`SDR-OTA-008`, `SDR-OTA-009`, `SDR-MOD-007`