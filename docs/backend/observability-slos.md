# Observability & Initial SLO Baseline

Observability must make business-state failures diagnosable across API, background jobs, signing, deployment and edge reconciliation. Metrics are useful only when they map to actionable runbooks and customer impact.

## Golden signals

- availability
- latency
- error rate
- saturation
- queue/backlog age and depth
- dependency health
- workflow completion/failure rate

## Proposed service indicators

| Capability | Indicator | Initial engineering target |
|---|---|---|
| Core LMS API | successful non-maintenance requests | 99.9% monthly SaaS |
| Read API | p95 latency | < 500 ms excluding artifact transfer |
| Write API | p95 latency | < 1 s excluding signing/package generation |
| Signing request | p95 under normal load | < 2 s |
| Audit append | persistence success | 99.99% |
| Deployment orchestration | state survives restart | 100% durable |
| Background jobs | oldest normal-priority pending age | product/runbook threshold |
| Offline reconciliation | unreconciled receipt age | visible by policy/site |

These are engineering baselines, not contractual SLAs. Business/operations must approve final targets before external commitments.

## Required metrics

### API
- request count/latency/status/error code by endpoint/module
- auth failure/rate limit
- tenant authorization denial count
- DB pool/query saturation

### Licensing
- entitlement/allocation/grant mutation success/failure
- signing pending/failure
- grant issued/delivered/accepted lag
- stale check-in and grace/restricted device counts
- renewal queue and expiry counts

### Release/deployment
- jobs/targets by state
- install success/failure/rollback rate
- rollback failure
- artifact download/hash/signature failure
- rollout pause/stop triggers

### Capacity
- assessment pass/warn/fail/stale
- benchmark-profile missing/low-confidence
- reassessment rate
- local versus central outcome divergence

### Infrastructure/dependencies
- PostgreSQL health/storage/connections
- artifact repository latency/error/capacity
- signing provider latency/error
- SMTP/ERP/telemetry dependency failures
- backup age/failure
- outbox/job queue depth/dead letters

## Logs

Structured JSON logs include UTC timestamp, level, request/correlation ID, module, tenant-safe object IDs, operation, result and stable error code. They exclude passwords, tokens, signing keys, unwrapped model keys and decrypted models.

## Tracing

Trace/correlation context propagates from API through application service, DB/outbox/job, signing/artifact dependency and deployment orchestration where supported. Edge receipts/check-ins carry identifiers that allow cross-boundary correlation even without distributed tracing.

## Alerting

Alerts should be symptom/customer-impact oriented: signing unavailable, DB unavailable, dead-letter growth, rollback failure, backup stale, cross-tenant anomaly, release signature failures or large stale-check-in spike. Every paging alert maps to an owner/runbook.

## SLO governance

Each SLO defines measurement window, exclusions, data source, owner and error-budget response. Targets are revisited after production measurements rather than silently changed to fit observed behavior.