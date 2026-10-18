# ADR-012 — Central Capacity Advisory, Local Capacity Authoritative

**Status:** Approved  
**Decision class:** Capacity / Edge Architecture

## Context

Central LMS can plan using reported inventory and benchmark profiles but cannot always see instantaneous streams, resource pressure, driver state or thermal conditions. Commercial entitlement must also remain distinct from hardware feasibility.

## Decision

Central Capacity Engine SHALL provide advisory pre-assessment. Local Capacity Engine SHALL make the authoritative activation decision using current local workload/runtime evidence.

Capacity failure SHALL NOT silently modify purchased entitlement. The engine returns recommendations and the operator/customer selects an allowed active configuration.

## Alternatives considered

### Central-only authority
Rejected because evidence can be stale and disconnected devices require local decisions.

### Capacity automatically rewrites license quantity
Rejected because technical feasibility and commercial rights are separate domains.

## Consequences

- safer runtime activation
- consistent offline behavior
- central UI can plan but must show freshness/confidence
- local and central assessment contracts must be compatible
- support must distinguish entitlement from selected active configuration

## Related requirements

`SDR-CAP-001` through `SDR-CAP-011`