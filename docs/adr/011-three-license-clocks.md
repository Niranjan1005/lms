# ADR-011 — Separate Commercial Expiry, Offline Freshness and Grace

**Status:** Approved  
**Decision class:** Licensing / Lifecycle

## Context

Subscription expiry, permitted disconnected operation and post-expiry recovery/grace answer different business/technical questions. Combining them into one timestamp would allow check-ins to accidentally extend paid rights or make offline behavior ambiguous.

## Decision

LMS SHALL model three independent clocks: commercial term/expiry, offline authorization freshness and grace/restriction period.

A successful check-in may refresh offline authorization only; it SHALL NOT extend commercial expiry. Renewal requires a new commercial term and signed grant revision.

## Alternatives considered

### One rolling expiry timestamp
Rejected because check-in could inadvertently renew commercial rights.

### No offline freshness limit
Rejected because indefinitely disconnected grants weaken revocation/control.

## Consequences

- predictable offline behavior
- clear renewal semantics
- separate policy configuration
- UI/support must display all clocks independently
- tests must cover combinations of active/expired/stale/grace

## Related requirements

`SDR-LIF-001` through `SDR-LIF-009`