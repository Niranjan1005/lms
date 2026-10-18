# Database Migration Policy

Database evolution must remain safe across SaaS and customer-hosted deployments, including delayed customer upgrades and application rollback constraints.

## Principles
- Alembic is the only supported production schema migration path.
- Schema changes are reviewed like application code.
- Migrations are repeatable at deployment orchestration level and observable.
- Destructive removal is delayed until all supported application versions stop using the old structure.
- Customer-hosted sites must never require ad-hoc manual SQL in a normal release.
- Migration compatibility is part of the release manifest/support window.

## Change classes
| Change | Typical approach |
|---|---|
| add nullable column/table/index | expand |
| make field mandatory | add/backfill/verify, then constrain later |
| rename field/table | dual read/write or compatibility view, then contract |
| large backfill | resumable/background migration with progress evidence |
| destructive drop | final contract release after support window |
| index on large table | online/concurrent approach where supported and tested |

## Expand-and-contract
~~~text
Release N   : add new structure; old application remains compatible
Release N+1 : dual-write/backfill/verify
Release N+2 : switch reads and stop old writes
Release N+3 : remove old structure after supported-version window
~~~

## Migration design requirements
Every material migration documents source/target schema versions, expected duration/data volume, lock/availability impact, transaction strategy, backfill/restart behavior, rollback/forward-recovery compatibility, monitoring/progress metric, failure recovery and customer-hosted supported source versions.

## Long-running migrations
Large data backfills should not hold one application deployment/DB transaction indefinitely. Prefer resumable idempotent jobs with checkpoints and verification before enabling a final constraint/contract step.

## Rollback
Application rollback is allowed only when the target older application can safely operate on the migrated schema. If not, the release is declared forward-fix only and deployment/runbook must state that explicitly before Stable promotion.

## Customer-hosted upgrades
Release package declares minimum/maximum supported source app/schema versions. Unsupported jumps are blocked and LMS provides the required intermediate upgrade path rather than attempting an unknown migration.

## Testing
CI/integration tests cover clean install and upgrade from supported baseline. Risky changes additionally test realistic data volume, interruption/restart, rollback compatibility and repeated orchestration invocation.

## Backup and evidence
High-risk migration requires verified backup/recovery readiness. Deployment records source/target schema version, migration IDs, duration, result and failure/recovery actions.