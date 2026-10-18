# Initial Work Breakdown Structure

The following epics provide a practical starting backlog aligned with architecture boundaries.

## Epic A — Platform foundation

- repository/project scaffolding
- configuration/secrets abstraction
- DB/Alembic baseline
- common ID/time/error/audit primitives
- development username/password auth
- RBAC/scope enforcement

## Epic B — Customer, site and device

- customer/site CRUD
- device ownership/site assignments
- enrollment authorization
- device registration
- hardware inventory upload
- transfer/rehost/decommission

## Epic C — Licensing core

- product/feature catalog
- entitlement pools
- allocations/reallocation transaction
- policy resolution
- grant canonicalization/signing integration
- local License Agent contract
- renewal/check-in/grace/revocation

## Epic D — Capacity

- inventory normalization
- benchmark profile model
- workload model
- central assessment
- local assessment contract
- recommendation engine

## Epic E — Marketplace

- feature listing/detail
- eligibility
- dynamic trial policies/campaigns
- purchase-request workflow
- approval screens

## Epic F — Release & OTA

- artifact repository abstraction
- release/model manifests
- release channels
- deployment jobs/targets
- auto/manual policy and maintenance window
- edge Update Manager
- health check and release-set rollback

## Epic G — Offline operations

- request export schema
- central import validation
- minimal bundle builder
- signed response package
- local import
- receipt export/reconciliation

## Epic H — Governance & operations

- notifications
- audit explorer
- monitoring/metrics
- backups/restore
- VAPT gates
- ERP adapter contract

Each epic should be decomposed into vertical slices that include backend, edge/UI, tests, audit and documentation rather than deferring integration until the end.