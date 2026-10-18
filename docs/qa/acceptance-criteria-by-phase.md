# Acceptance Criteria by Delivery Phase

These are minimum exit criteria for phase completion; detailed stories may add stricter criteria.

## Phase 1 — Trust foundation

- device generates/loads protected key pair
- enrollment rejects invalid/reused authorization
- signed grant verifies offline
- wrong-device/tampered/expired/stale-revision grants are rejected
- last-known-time rollback scenario is covered by tests
- audit events exist for enrollment and issuance

## Phase 2 — Registry & licensing

- customer/site/device topology supports multi-site server assignment
- entitlement pool cannot be over-allocated
- reallocations supersede affected device grants
- base/add-on dependency works
- subscription and perpetual terms represented without schema change
- decommission returns rights to pool

## Phase 3 — Capacity

- stable inventory separated from resource snapshots
- benchmark profile/version recorded in assessment
- combined existing+proposed workload evaluated
- warning/fail produces recommendations
- commercial quantity remains unchanged on capacity failure

## Phase 4 — Marketplace & release management

- marketplace hides/disables ineligible actions with reason
- trial duration can be configured
- trial starts only after successful activation
- Stable/LTS channel rules enforced
- release manifest is immutable and signed
- unsupported dependency/OS/runtime is blocked

## Phase 5 — Model OTA & deployment

- installed model inventory prevents unnecessary redownload
- encrypted model cannot be used without authorization
- model-only OTA supported
- automatic/manual modes supported
- default maintenance window 01:00–03:00 and override works
- failed health check restores previous coherent release set

## Phase 6 — Lifecycle

- commercial expiry, offline validity and grace behave independently
- check-in does not extend commercial term
- offline renewal can be imported and reconciled
- revocation behavior is correct for online and air-gapped cases
- major identity change triggers rehost flow

## Phase 7 — Hardening

- backup restore successfully rehearsed
- VAPT findings triaged/remediated per release policy
- tenant-isolation tests pass
- monitoring/alerts cover critical workflows
- operational and support runbooks reviewed
- production readiness checklist signed off