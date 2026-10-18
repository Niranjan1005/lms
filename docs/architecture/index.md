# Architecture Overview

LMS is a modular enterprise control plane. Central services own commercial and lifecycle truth; protected signing establishes verifiable authorization; edge components enforce actual runtime authorization, capacity and installation health.

## System view
~~~mermaid
flowchart TB
    P[Admin / Customer Portal] --> API[Central LMS API]
    API --> REG[Registry & Enrollment]
    API --> ENT[Entitlement / Allocation]
    API --> POL[Policy Engine]
    API --> CAP[Central Capacity]
    API --> MKT[Marketplace]
    API --> REL[Release / Model / Deployment]
    API --> LIFE[Renewal / Check-in / Revocation]
    API --> AUD[Audit / Notifications]
    ENT --> LS[Protected License Signing]
    REL --> RS[Protected Release Signing]
    REL --> AR[(Artifact Repository)]
    API --> DB[(PostgreSQL)]
    API -->|Online| EDGE[Edge / Server]
    API -->|Signed request-response| RELAY[Relay / Controlled Media]
    RELAY --> EDGE
    EDGE --> ID[Device Identity]
    EDGE --> LA[License Agent]
    EDGE --> LC[Local Capacity Engine]
    EDGE --> UM[Update Manager]
    EDGE --> RT[Analytics Runtime]
~~~

## Architecture principles
1. Registration, licensing, capacity and installation/health are separate states.
2. Entitlement is commercial truth; Grant is signed executable authorization.
3. Central capacity is advisory; local capacity is authoritative for activation.
4. Marketplace/request/payment state does not by itself authorize execution.
5. Signing private keys remain outside normal LMS application/database storage.
6. Online and offline routes preserve the same cryptographic trust semantics.
7. PostgreSQL stores transactional metadata; large binaries use an external artifact repository.
8. Edge updates commit coherent Release Sets and rollback autonomously on health failure.
9. SaaS and customer-hosted use the same core application/domain codebase.
10. ERP and high-volume telemetry remain separate systems of record from operational licensing truth.

## Responsibility split
| Domain | Central responsibility | Edge responsibility |
|---|---|---|
| Identity | customer/device registry, public key binding | private key protection, fingerprint evidence |
| Licensing | entitlement/allocation/policy/grant issuance | signature/time/revision/constraint enforcement |
| Capacity | benchmark-based planning/recommendation | current workload authoritative validation |
| Release | catalog/release/model/deployment orchestration | verify/stage/migrate/health/commit/rollback |
| Offline | validate/build signed response | build signed request, verify/import, receipt |
| Lifecycle | renewal/revoke/transfer/rehost policy | accept signed state and enforce locally |

## Failure-domain philosophy
Dependency failures do not mutate unrelated truth. Email failure does not undo renewal; artifact outage does not remove entitlement; signing outage blocks new issuance but not valid grants; telemetry outage does not invalidate licensing.

## Normative references
System Design Requirements defines testable behavior. ADRs explain durable architecture choices. Trust Boundaries, Deployment Models and sequence/state-machine pages define implementation interactions.