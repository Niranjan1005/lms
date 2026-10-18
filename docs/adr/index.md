# Architecture Decision Records

ADRs document durable architecture decisions, the problem that forced each decision, alternatives rejected, consequences, security/operational impact and follow-up work. They are not one-line summaries and they are not substitutes for requirements.

## Decision register

| ADR | Decision | Status | Primary domain |
|---|---|---|---|
| ADR-001 | Digitally Signed Device-Bound Grants | Approved | Licensing / Security |
| ADR-002 | Modular Monolith First | Approved | Backend |
| ADR-003 | Marketplace & OTA Inside LMS | Approved | Product / Platform |
| ADR-004 | Traditional Signed Edge Release Packages | Approved | Edge / Release |
| ADR-005 | Device-Generated Cryptographic Identity | Approved | Device / Security |
| ADR-006 | Separate License and Release Signing Keys | Approved | Security |
| ADR-007 | Signed Offline Request/Response Protocol | Approved | Offline / Security |
| ADR-008 | Production Human Authentication | Open Decision | Identity |
| ADR-009 | Model Encryption and Key Wrapping | Open Security Decision | Model Security |
| ADR-010 | Release Package Format | Proposed | Edge / Packaging |
| ADR-011 | Separate Commercial Expiry, Offline Freshness and Grace | Approved | Licensing Lifecycle |
| ADR-012 | Central Capacity Advisory, Local Capacity Authoritative | Approved | Capacity / Edge |
| ADR-013 | Transactional Outbox for External Side Effects | Approved | Backend Reliability |
| ADR-014 | External Artifact Repository, PostgreSQL Metadata Only | Approved | Storage / Release |
| ADR-015 | Coherent Release Set as Deployment/Rollback Unit | Approved | OTA / Edge |
| ADR-016 | Tenant Isolation Enforced in Application Authorization | Approved | Security / SaaS |
| ADR-017 | Separate High-Volume Telemetry from Licensing OLTP | Approved | Data / Operations |
| ADR-018 | Same Core LMS Codebase for SaaS and Customer-Hosted | Approved | Deployment |

## ADR status meanings

**Proposed** — candidate decision under review; implementation should not rely on it as immutable baseline yet.

**Approved** — normative architecture baseline. Changes require a superseding ADR or explicit amendment process.

**Open Decision** — problem/constraints are known but the final choice is intentionally unresolved. Implementation must preserve the documented abstraction.

**Deprecated / Superseded** — retained for history; a newer ADR is authoritative.

## When an ADR is required

Create or supersede an ADR when a change materially affects:
- trust boundary or cryptographic design
- authentication/authorization model
- core licensing semantics
- deployment topology/codebase strategy
- persistence/storage architecture
- public/local API compatibility strategy
- update/package format or rollback model
- offline trust protocol
- major module decomposition or cross-module consistency model
- telemetry/operational source-of-truth architecture

A normal implementation detail, bug fix or UI copy change does not require an ADR unless it changes one of those durable decisions.

## Required ADR content

~~~text
# ADR-XXX — Title

Status: Proposed | Approved | Open Decision | Superseded
Decision class: <domain>
Date: YYYY-MM-DD

## Context
Why the decision is needed; forces/constraints.

## Decision
Normative choice and boundaries.

## Alternatives considered
Serious alternatives and why they were rejected/deferred.

## Consequences
Positive outcomes, costs, risks and migration implications.

## Security / operational impact
Where relevant.

## Related requirements
SDR IDs and handbook sections.

## Follow-up / decision deadline
Implementation work or unresolved choices.
~~~

## Supersession rule

Approved ADRs are historical records. Do not silently rewrite their fundamental decision after implementation. If the architecture changes materially, create a new ADR that states `Supersedes: ADR-XXX`, update this index, and preserve the old record.

Clarifying detail may be added to an existing ADR only when it does not reverse or materially change the approved decision.

## Traceability

Every approved ADR should map to relevant SDR requirements, implementation epics/issues and verification evidence. SDR states **what the system SHALL do**; ADR states **why this architecture was chosen**.