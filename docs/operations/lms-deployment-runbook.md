# LMS Deployment & Upgrade Runbook

## SaaS deployment

1. Confirm release approval and backup/recovery readiness.
2. Apply DB-compatible release using controlled deployment.
3. Run migrations before/with application start according to migration contract.
4. Verify API, DB, signing, artifact repository, notification and background-job health.
5. Run smoke tests for login, device check-in, grant issuance in safe test scope and artifact access.
6. Monitor errors/latency/queues after release.
7. Roll back application when safe; do not blindly downgrade incompatible schema.

## Customer-hosted deployment

1. Validate supported source LMS version and environment prerequisites.
2. Take verified backup of DB/artifact/config state.
3. Verify signed vendor LMS package.
4. Stop/coordinate services according to maintenance procedure.
5. Execute automated application/migration package.
6. Run health checks.
7. Validate customer portal, device check-in and artifact/signing integration.
8. Complete upgrade receipt/runbook record.

## Failure handling

If migration/app startup fails, follow the release-specific recovery path. Never hand-edit production schema unless an approved emergency procedure explicitly requires it and captures the exact changes.

## Rollback decision

Rollback feasibility is declared by the release. When DB migration is backward-compatible, application rollback may proceed. When not, use forward-fix/recovery procedure rather than unsafe schema downgrade.

## Post-deployment evidence

Record release ID, operator, start/end time, source/target versions, migration result, health result, exceptions and rollback status.