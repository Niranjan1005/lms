# Implementation Phases

Phases are dependency-ordered capability increments. A phase is not complete because code exists; it must satisfy the corresponding exit criteria and integration evidence.

## Phase 1 — Trust foundation

Device identity/key storage, enrollment authorization, grant canonicalization/signing/verifier, trust-store/key-purpose separation and anti-replay/rollback foundations.

## Phase 2 — Registry & licensing

Customer/site/device topology, RBAC/tenant scope, entitlement pools, allocations, base/add-on grants, audit and online base activation.

## Phase 3 — Hardware & capacity

Stable inventory, dynamic snapshots, workload model, benchmark governance, central advisory assessment, local authoritative assessment and recommendations.

## Phase 4 — Marketplace & release management

Product/feature catalog, trial/purchase request, artifact repository, release channels, signed release manifests, compatibility/dependency metadata and portal flows.

## Phase 5 — Model OTA & deployment

Encrypted model lifecycle, model inventory, release sets, online deployment jobs, AUTO/MANUAL policy, maintenance windows, health-check, rollback and model-only OTA.

## Phase 6 — Lifecycle & offline

Renewal, three clocks, check-in, grace/restriction, revocation, rehost/transfer/decommission, assisted-offline and fully air-gapped request/response/receipt flows.

## Phase 7 — Hardening & production readiness

Production IAM decision, VAPT, supply-chain controls, key rotation/recovery exercise, performance/resilience tests, DR/restore exercise, monitoring/alerts, runbooks/support, ERP reconciliation and production approval.

## Dependency principle

Do not defer edge integration/offline/security to the final phase. Each earlier phase includes the minimum edge, audit, authorization and test work needed to prove its vertical slice. Phase 7 hardens completed capabilities rather than discovering integration for the first time.