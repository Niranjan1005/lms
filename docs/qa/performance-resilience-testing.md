# Performance, Load & Resilience Testing

Functional correctness alone is insufficient for production readiness.

## Central LMS tests

- API latency under expected and peak concurrency
- entitlement/allocation transaction contention
- signing throughput and degraded signing-provider behavior
- deployment orchestration at fleet scale
- background-job backlog/recovery
- artifact metadata operations
- audit-event volume
- tenant-isolation under concurrent load

## Edge tests

- steady-state analytics with licensed maximum workload
- combined feature workloads
- update while under normal workload
- model switch/warm-up
- low disk/memory conditions
- service restart/power interruption during install
- rollback under failure
- long offline duration within policy

## Soak tests

Long-running tests detect memory leaks, queue growth, resource drift, thermal throttling and repeated check-in/telemetry behavior.

## Fault injection

Exercise recoverable failures such as DB reconnect, artifact-store timeout, signing-service outage, network loss, corrupted package, process crash and interrupted offline import.

## Exit evidence

Record environment, versions, load model, thresholds, measured p50/p95/p99, error rate, recovery behavior and known limits. Performance regressions against approved baseline are release-blocking when they violate product/SLO targets.