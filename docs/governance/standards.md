# Engineering & Documentation Standards

## Engineering

- Typed Python where practical.
- Pydantic at API boundaries.
- Alembic only for production schema changes.
- Structured logs with correlation IDs.
- Explicit domain/service boundaries.
- Authorization tests for tenant-scoped data.
- Idempotency for retried workflows.
- No secrets in source control.

## Documentation

- Behaviour-changing PRs update the handbook.
- Approved/proposed/open-decision status is explicit.
- Mermaid is preferred for maintainable diagrams.
- Material architecture changes require ADRs.
- Real customer data is never used in examples.