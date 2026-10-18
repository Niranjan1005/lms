# Database Migration Policy

Database evolution must be safe across SaaS and customer-hosted deployments.

## Rules

- Alembic is the only supported schema migration path.
- Production schema changes are reviewed like application code.
- Destructive migrations are never combined with the first release that stops using the old field/table.
- Prefer expand-and-contract for risky changes.
- Migrations must be idempotent at deployment orchestration level and never require manual SQL at customer sites.

## Expand-and-contract example

~~~text
Release N: add new nullable column/table + dual-read/write where needed
Release N+1: backfill/verify + switch reads
Release N+2: stop writing old field
Release N+3: remove old field after support window
~~~

## Rollback

Before Stable promotion, verify whether application rollback is compatible with the migrated schema. If schema rollback is unsafe, the release must use backward-compatible migration design rather than assuming DB downgrade.

## Customer-hosted

Each release package declares supported source schema versions and target schema version. Update Manager blocks unsupported upgrade jumps and provides a clear required intermediate version.