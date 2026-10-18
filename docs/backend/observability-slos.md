# Observability & Initial SLO Baseline

SLOs below are proposed engineering targets and must be finalized with business/operations before production launch.

## Golden signals

- availability
- latency
- error rate
- saturation
- queue/backlog depth
- external dependency health

## Proposed service indicators

| Capability | Indicator | Initial target |
|---|---|---|
| Core LMS API | successful non-maintenance requests | 99.9% monthly SaaS |
| Read API latency | p95 | < 500 ms excluding artifact transfer |
| Write API latency | p95 | < 1 s excluding signing/package build |
| Signing request | p95 | < 2 s under normal load |
| Audit persistence | successful append | 99.99% |
| Deployment orchestration | state not lost across restart | 100% durable |

## Required telemetry

- structured JSON logs with request/correlation ID
- metrics per endpoint/module/error code
- distributed trace context at central service boundaries
- signing gateway latency/failure metrics
- artifact storage latency/error metrics
- deployment success/rollback rates
- renewal/check-in backlog

No secrets, private keys, raw passwords or decrypted model material may appear in logs.