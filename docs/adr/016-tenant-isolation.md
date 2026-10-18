# ADR-016 — Tenant Isolation Enforced in Application Authorization

**Status:** Approved  
**Decision class:** Security / SaaS Architecture

## Context

SaaS LMS is multi-tenant. Customer/site/device identifiers are externally supplied in APIs and cannot be trusted as proof of access. Customer-hosted mode may be single-customer, but maintaining separate code paths would increase security drift.

## Decision

Tenant/customer scope SHALL be enforced in authorization and repository/service access paths for all business data, including background jobs, audit queries, offline package generation and deployment targeting.

Customer-hosted mode SHALL keep the same tenant-aware code paths even when only one customer is configured.

## Alternatives considered

### UI-only filtering
Rejected because direct API/object-ID access could bypass it.

### Separate tenant-specific databases as the only isolation control
Rejected as the sole control because application authorization is still required and SaaS/customer-hosted topology may vary.

### Remove tenant checks in customer-hosted mode
Rejected because divergent code paths would create regression/security risk.

## Consequences

- repository/service interfaces require scope context
- negative tenant-isolation tests are release blockers
- global/support access must be explicit rather than accidental
- background workers must carry tenant identity

## Related requirements

`SDR-BE-009`, `SDR-SEC-001`, `SDR-SEC-007`