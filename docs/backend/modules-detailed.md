# Backend Modules — Detailed Responsibilities

This page defines the initial modular-monolith boundaries. Modules may share one deployable process and database while maintaining explicit ownership and service interfaces.

## Identity & Access

Responsibilities:
- development username/password authentication
- session/token issuance
- role and permission evaluation
- tenant/customer scope enforcement
- future OIDC/SSO adapter boundary

Must not:
- own commercial entitlement logic
- directly mutate device grants

## Customer, Site & Topology

Responsibilities:
- customer lifecycle
- site lifecycle and timezone
- device ownership relationships
- device-to-site assignments including multi-site server topology
- transfer/decommission coordination

Key invariants:
- a device has one commercial owner at a time
- site assignments are explicit and auditable
- transfer never silently overwrites previous ownership

## Device Enrollment

Responsibilities:
- enrollment authorization creation
- single-use/short-lived enrollment token validation
- public-key registration
- fingerprint version validation
- duplicate/prior-registration detection
- initial hardware inventory capture

Outputs a registered device identity only; registration does not grant paid rights.

## Catalog

Responsibilities:
- products
- features
- dependencies
- compatibility metadata
- marketplace visibility
- release/model associations

## Entitlements

Responsibilities:
- commercial rights
- subscription/perpetual term
- entitlement pools
- update-right policy
- ERP synchronization boundary

Entitlements are customer-owned business truth and are not directly executable on a device.

## Allocation

Responsibilities:
- distribute pooled quantities to device/site scopes
- validate total quantity
- support reallocation
- create a stable snapshot used for grant generation

Reallocation affecting multiple devices must be transactionally coordinated.

## Policy Engine

Responsibilities:
- trial duration
- offline validity
- grace
- update rights
- co-termination
- release-channel eligibility
- override hierarchy
- maker-checker requirement determination

Resolution hierarchy is explicit and deterministic: platform -> product -> customer/entitlement -> site/device exception where supported.

## Grant Service

Responsibilities:
- construct canonical device-bound grant payload
- resolve dependencies and constraints
- revision and supersession
- signing request
- issuance record
- delivery/reconciliation state

Signing private-key operations are delegated to the signing boundary.

## Capacity Service

Responsibilities:
- inventory normalization
- benchmark lookup
- current+proposed workload calculation
- feasibility result
- recommended alternatives
- assessment evidence/versioning

Must never mutate commercial entitlement automatically.

## Marketplace

Responsibilities:
- feature discoverability
- customer/device eligibility
- trial/purchase initiation
- capacity preview
- current entitlement and release readiness view

## Release & Artifact Management

Responsibilities:
- feature/application/UI/runtime releases
- release channels
- signed manifest metadata
- artifact repository references
- compatibility/dependency graph
- release-set composition

## Model Management

Responsibilities:
- model identity/version
- encryption metadata
- compatibility
- model-only OTA
- device model inventory reconciliation

## Deployment Orchestration

Responsibilities:
- target selection
- automatic/manual policy
- maintenance-window scheduling
- concurrency
- per-device state
- retry policy
- rollback observation
- installation receipt reconciliation

## Lifecycle

Responsibilities:
- renewal reminders
- commercial renewal workflow
- offline check-in freshness
- grace/restriction
- revocation
- rehost
- decommission

## Audit & Notification

Audit is append-only for privileged and business-significant events. Notification starts with portal + email and retains an adapter boundary for webhooks.