# Monitoring & Operational Integration

ERP contract details live in the Integrations section. This page defines operational monitoring responsibilities.

## Core health

Monitor:
- LMS API availability, latency and error rate
- PostgreSQL connection/replication/storage health as applicable
- background-job queue depth and oldest age
- outbox pending/dead-letter count
- signing-provider latency/failures
- artifact repository latency/errors/capacity
- authentication failure/rate-limit anomalies
- notification delivery failures
- backup success/age
- deployment success/failure/rollback rate
- device check-in freshness distribution
- renewal/trial processing backlog
- capacity assessment warning/fail/stale rate
- ERP reconciliation mismatch/failure

## Alert classes

| Condition | Example action |
|---|---|
| API unavailable/high error | Operations incident triage |
| Signing unavailable | Stop manual retries; queue issuance; escalate if customer impact |
| Dead-letter growth | inspect worker/dependency; replay only with approved procedure |
| Backup stale/failed | immediate operations investigation |
| Rollback failure | high-severity release incident |
| Tenant/authz anomaly | security escalation |
| Check-in stale spike | connectivity/systemic device investigation |
| ERP mismatch spike | integration/commercial reconciliation |

## Dashboards

Minimum production dashboards cover API/service health, DB/dependencies, signing, deployments, jobs/outbox, licensing lifecycle, capacity and backup status.

## Logging and correlation

Central logs are structured and include request/correlation ID, tenant-safe object identifiers and stable error codes. Sensitive values remain redacted.

## ERP monitoring boundary

ERP may be authoritative for orders/invoice/payment/contracts. LMS remains authoritative for operational entitlements, allocations, grants, activation, deployment and local acceptance. Integration failure is visible and reconciled; it does not silently rewrite either system.