# Engineering & Documentation Standards

These standards define the minimum implementation discipline for LMS. Module-specific standards may be stricter.

## Code

- Python 3.12 baseline for backend/central services unless superseded by ADR
- typed Python for public/module boundaries and non-trivial domain code
- Pydantic at external/API/event boundaries
- SQLAlchemy/Alembic for persistence/migrations
- explicit domain/application/repository separation where it improves ownership/testability
- no hidden cross-module database writes
- deterministic IDs/time handling through shared primitives
- UTC persistence; site timezone only for display/scheduling interpretation

## API and contracts

- `/v1` versioned API baseline
- stable machine-readable error codes
- request/correlation IDs
- idempotency on retryable writes
- cursor/bounded pagination for large collections
- backward compatibility within major version
- generated OpenAPI becomes executable contract once implementation begins

## Database

- migrations through Alembic only
- FK/unique/check constraints enforce invariants where possible
- optimistic concurrency for mutable aggregates
- transactional business invariants
- expand-and-contract for destructive evolution
- query/index decisions validated against production-like plans before launch

## Security

- deny-by-default authorization
- tenant/object scope validation server-side
- no secrets/private keys in source
- approved crypto libraries only
- signed/package parsers fail closed
- sensitive logs redacted
- threat/negative tests for trust boundaries

## Reliability

- external side effects use durable outbox/jobs where atomic DB participation is impossible
- consumers/actions are idempotent
- retries are bounded and observable
- dead-letter state is visible and recoverable
- no silent data correction for commercial truth mismatches

## Testing

- unit + integration + contract + security negative tests as appropriate
- tenant isolation is release blocking
- migration/upgrade/rollback tests for release-impacting changes
- representative edge hardware validation for capacity/update changes

## Observability

- structured logs
- metrics for latency/error/saturation/backlog
- request IDs across API/job/audit flows
- alerts map to operational runbooks

## Documentation

- behavior-changing PR updates handbook in same PR
- SDR requirements updated when normative behavior changes
- material architecture changes require ADR
- statuses Approved/Proposed/Open Decision/Superseded are explicit
- examples use synthetic data
- diagrams use maintainable Mermaid where practical

## Pull-request quality

A PR explains problem, affected SDR/ADR, implementation, API/schema/migration impact, security/tenant impact, test evidence, rollback/compatibility and documentation changes.

## Prohibited shortcuts

- production secrets in source/docs
- UI-only authorization
- manual DB schema changes as normal release procedure
- unsigned executable update content
- customer-specific hard-coded feature columns
- swallowing background-job/deployment failures without state/audit evidence