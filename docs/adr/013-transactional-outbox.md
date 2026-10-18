# ADR-013 — Transactional Outbox for External Side Effects

**Status:** Approved  
**Decision class:** Backend Reliability

## Context

Grant signing, notifications, ERP synchronization and deployment dispatch depend on external systems that cannot join a PostgreSQL transaction. Performing them inline can leave commercial state inconsistent if the network call succeeds/fails at the wrong time.

## Decision

Persist business state and an outbox event in the same database transaction. Durable workers deliver external side effects with at-least-once semantics; consumers/actions must be idempotent.

## Alternatives considered

### Direct external call inside request transaction
Rejected because external systems cannot participate atomically and long calls hold DB/request resources.

### Fire-and-forget in memory
Rejected because process restart loses work.

## Consequences

- durable recovery from dependency outages
- explicit retry/dead-letter handling
- duplicate delivery must be tolerated
- operational monitoring of queue age/dead letters is mandatory

## Related requirements

`SDR-BE-003`, `SDR-BE-004`, `SDR-BE-005`