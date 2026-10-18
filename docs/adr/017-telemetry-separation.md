# ADR-017 — Separate High-Volume Telemetry from Licensing OLTP

**Status:** Approved  
**Decision class:** Data / Operations Architecture

## Context

Licensing, entitlement, grant and audit records require transactional integrity. Usage/performance telemetry can be high-volume, delayed and best-effort. Mixing both concerns in the same operational path would increase database pressure and make licensing dependent on analytics delivery.

## Decision

Transactional licensing/audit state SHALL remain in the operational PostgreSQL data model. High-volume telemetry SHALL be logically separated and MAY move to a dedicated time-series/analytics/warehouse store as volume requires.

Licensing SHALL NOT depend on successful delivery of best-effort high-volume telemetry.

## Alternatives considered

### Put all telemetry in core OLTP indefinitely
Rejected due to scaling/retention/query interference risk.

### Make telemetry receipt mandatory for license validity
Rejected because offline/air-gapped operation is a first-class requirement.

## Consequences

- clear operational source of truth
- telemetry pipelines can evolve independently
- duplicated/aggregated operational events may exist in analytics
- privacy/residency policy remains separately governable

## Related requirements

`SDR-TEL-001`, `SDR-TEL-002`, `SDR-TEL-003`