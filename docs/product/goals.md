# Goals & Non-Goals

## Product mission

Make offline and customer-hosted enterprise AI deployments scalable, governable and monetizable through one control plane for identity, commercial rights, capacity, feature delivery and lifecycle.

## Goals

### Reusable control plane
One licensing/marketplace/lifecycle platform serves AI-BOX, FR Server and future product families without cloning business logic per product.

### Commercial flexibility
Support subscription and perpetual bases, pooled quantities, device/site allocation, add-ons, trials, renewals and explicit update rights without feature-specific schema columns.

### Offline-first trust
Online, assisted-offline and fully air-gapped deployments use the same cryptographic trust semantics and can verify authorization locally.

### Device lifecycle
Register device identity independently from licensing; support multi-site assignments, rehost, transfer, replacement, revocation and decommission with auditable lineage.

### Hardware feasibility
Assess combined workloads using inventory + benchmark evidence, keep capacity separate from entitlement, and let local runtime make authoritative activation checks.

### Marketplace and delivery
Provide discover/try/buy experience integrated with entitlement/capacity state and deliver signed application/model release sets with migration, health and rollback.

### Model lifecycle
Treat AI models as independent versioned, encrypted, signed and inventory-aware artifacts with model-only OTA where compatible.

### Corporate governance
Provide tenant isolation, RBAC, maker-checker, audit, security logging, release approvals, backup/restore, incident/support runbooks and VAPT readiness.

### Deployment flexibility
Run the same core LMS codebase as SaaS or customer-hosted with provider/configuration adapters.

## Success indicators

The architecture is successful when a new product/feature can be onboarded through metadata/policy/contracts rather than schema forks; an offline device can independently verify its authorization and updates; pooled rights can be safely reallocated; updates can roll back autonomously; and support can determine exact commercial, grant, capacity and installation state from auditable evidence.

## Phase 1 non-goals

- building a full ERP/accounting system
- Windows-first edge implementation
- mandatory Kubernetes/microservices
- Docker as a required edge runtime dependency
- fully automatic self-upgrade of customer-hosted LMS
- unlimited offline authorization
- claiming software-only tamper-proof execution on a root-compromised host
- solving customer video/content analytics privacy beyond the explicitly approved telemetry scope

## Architectural non-goals

LMS does not make commercial entitlement equal to capacity, does not use package possession as license authorization, does not treat a relay as a signing authority, and does not make high-volume telemetry a prerequisite for license validity.