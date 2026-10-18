# ADR-002 — Modular Monolith First

**Status:** Approved  
**Decision class:** Backend Architecture

## Context

LMS spans registry, licensing, policy, capacity, marketplace, release, offline workflows, renewals, integrations and audit. Early microservice decomposition would add distributed transactions, deployment overhead and operational complexity before scale boundaries are proven.

## Decision

Implement the central Python/FastAPI platform as a modular monolith with explicit domain/module ownership and service interfaces.

Modules share one deployable process and PostgreSQL database initially but SHALL maintain clear internal boundaries so later extraction remains possible.

## Alternatives considered

### Microservices from day one
Rejected due to premature operational complexity, cross-service consistency risk and slower delivery.

### Unstructured monolith
Rejected because domain boundaries would erode and future extraction/testing would be harder.

## Consequences

### Positive
- simpler deployment/observability/transactions
- faster cross-domain iteration
- easier customer-hosted packaging
- strong transactional consistency for entitlement/allocation/grant workflows

### Negative / risk
- discipline is required to prevent module coupling
- scaling is process/database oriented initially
- module boundaries are architectural rather than infrastructure-enforced

## Rules

- controllers do not directly orchestrate unrelated modules
- cross-module actions use application/use-case services
- module ownership of tables/services/endpoints is documented
- internal events/outbox are used for asynchronous external side effects
- future extraction must preserve contracts rather than copy hidden dependencies

## Related requirements

`SDR-PLT-003`, `SDR-BE-003`, `SDR-BE-004`