# Product & Scope

LMS is the enterprise control plane for customer/device identity, commercial rights, capacity feasibility, feature discovery/delivery and edge lifecycle across connected, customer-hosted and air-gapped AI deployments.

## Product problem

Without a common control plane, every product tends to invent its own customer registry, licensing, trials, feature delivery, renewal and offline process. That makes enterprise deployment difficult to monetize, support and audit. LMS standardizes those concerns while leaving product analytics execution on the edge.

## Primary outcomes

- onboard customers/sites/devices once
- represent commercial rights generically
- allocate pooled rights without over-allocation
- issue device-bound signed authorization
- plan and validate real hardware capacity
- expose marketplace/trial/purchase workflows
- safely deliver application/model updates online/offline
- renew/revoke/rehost/transfer with auditable lifecycle state
- support SaaS and customer-hosted operations from one codebase

## Actors

| Actor | Primary responsibility |
|---|---|
| Vendor Super Admin | global platform/customer administration; high-risk governance |
| Product Admin | product/feature/commercial/trial policy |
| Release Manager | release promotion, rollout and rollback |
| Security Approver | security-sensitive approvals/key/trust actions |
| Developer | non-production development artifacts/code |
| Support Engineer | diagnostics/runbook/recovery within scoped permission |
| Customer Admin | customer sites/devices/allocations/trials/renewals/policies |
| Site Admin | site-scoped operations/workload/update visibility |
| Read-Only Auditor | audit/compliance visibility |
| Edge Device / Server | cryptographic identity, local verification/capacity/update/runtime |

## Ownership topology

~~~mermaid
flowchart TD
    C[Customer / Tenant] --> S1[Site A]
    C --> S2[Site B]
    C --> D[Owned Device / Server]
    D --> A1[Device-Site Assignment]
    A1 --> S1
    A1 --> S2
~~~

A device has one commercial customer owner at a time but may serve multiple sites through explicit assignments.

## Scope boundaries

### LMS owns
customer/site/device operational topology, entitlements, allocations, grants, trials, capacity evidence, marketplace state, release/model metadata, deployments, renewals/check-ins, offline exchange, notifications and audit.

### Edge owns
device private identity, actual runtime workload, local authorization enforcement, local capacity authority, install/health/rollback and signed receipts.

### ERP owns when integrated
orders, invoices/payment and contract financial truth. LMS imports approved commercial state but is not an accounting system.

## Critical separations

`Registered != Licensed != Capacity Validated != Installed/Healthy` and `Issued != Delivered != Accepted`. These distinctions are visible in APIs, portal and support workflows.

## Product non-goals

See Goals & Non-Goals. The platform does not promise software-only tamper-proof operation on a hostile root-owned device, does not require continuous internet, does not use telemetry as paid-license renewal, and does not silently reduce purchased rights because hardware is insufficient.

## Normative sources

System Design Requirements define testable SHALL requirements. ADRs explain durable architecture choices. Consolidated Business Rules define cross-domain commercial/lifecycle invariants.