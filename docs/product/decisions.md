# Approved Product & Architecture Decisions

This register summarizes current decisions. The detailed rationale lives in ADRs and domain sections; this page is a quick baseline and must not override a newer ADR.

| Area | Approved baseline | Rationale / implication |
|---|---|---|
| Backend | Python 3.12 + FastAPI modular monolith | transactional consistency and operational simplicity first |
| Database | PostgreSQL + SQLAlchemy + Alembic | relational commercial truth and controlled migrations |
| Portal | React + Vite + TypeScript | standard web admin/customer UI stack |
| Deployment | same core codebase for SaaS and customer-hosted | avoid product forks |
| Edge OS | Ubuntu/Linux first, Windows-compatible abstractions | current delivery priority without architectural dead-end |
| Human auth | local username/password for development only; production IAM is ADR-008 | do not couple RBAC to provider |
| Device identity | device-generated asymmetric key + versioned fingerprint | MAC is evidence, not identity |
| Grant model | entitlement -> allocation -> signed device grant | separate commercial right from execution |
| Trial | default 7 days, configurable, starts at first successful activation | no globally reusable trial license |
| Offline freshness | default 7 days, policy configurable | bounded disconnected authorization |
| Grace | default 7 days, independently configurable | separate recovery window from paid term |
| Add-ons | co-terminate with subscription base by default | independent exceptions explicit |
| Capacity | central advisory, local authoritative | hardware feasibility != commercial right |
| Package delivery | traditional signed release bundles; no Docker dependency | offline/Linux/Windows flexibility |
| Auto OTA | supported; Stable by default | company controls production channel |
| LTS | explicit designation only | not every Stable release becomes long-term support |
| Maintenance | default 01:00–03:00 site time | customer configurable |
| Rollback | coherent Release Set; previous known-good mandatory | app/model/config compatibility |
| Model OTA | independent, encrypted, signed, inventory-aware | model lifecycle separate from app |
| Artifact storage | external object/file repository; DB metadata only | avoid large BLOBs in PostgreSQL |
| Offline | signed request/response with nonce/device binding; relay transport-only | same trust model without connectivity |
| Audit retention | configurable 1–3 year baseline | corporate governance |
| ERP | separate financial system with idempotent synchronization | LMS is not accounting |
| Telemetry | separate from transactional licensing | licensing must survive telemetry outage |

## Defaults versus hard decisions

Trial/offline/grace durations and maintenance window are approved defaults but remain configurable policy. Cryptographic verification, tenant isolation, key separation and no-silent-rights-reduction are non-relaxable architecture/security principles.

## Open decisions

Production IAM profile, model key-wrapping implementation, final release archive format, telemetry privacy/residency/retention, enterprise HA/RTO/RPO, benchmark thresholds and historical support window remain explicitly open/proposed in their owning ADR/section.

## Change rule

Changing a durable architecture decision requires ADR review/supersession. Changing a configurable default requires product/policy approval plus regression/documentation update.