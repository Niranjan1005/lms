# Requirements Coverage Audit

This audit compares the engineering handbook against the agreed LMS product, architecture, licensing, marketplace, OTA, capacity, edge, security, QA and operations requirements.

**Audit result:** the original handbook was strong but had several material omissions. The gaps listed under "Corrected in this audit" have now been added. Remaining items are intentional open decisions, not undocumented requirements.

## Product and scope

| Requirement | Status | Handbook location |
|---|---|---|
| One control plane for current/future products | Covered | Product, Architecture |
| SaaS + customer-hosted from same codebase | Covered | Deployment Models, Customer-Hosted Topology |
| Modular FastAPI application first, not microservices | Covered | ADR-002, Backend |
| Registration != licensing != capacity validation | Covered | Home, Architecture, Business Rules |
| ERP separate from LMS | Covered | ERP Contract |
| Public/customer-hosted upgrade model | Covered | Customer-Hosted Topology |

## Licensing and lifecycle

| Requirement | Status | Handbook location |
|---|---|---|
| Entitlement -> Allocation -> Device-bound Grant | Covered | Licensing Overview, Entitlements |
| Subscription + perpetual | Covered | Business Rules, Policy Model |
| Base + independently identifiable add-ons | Covered | Trials & Add-ons |
| Default add-on co-termination | Covered | Trials & Add-ons |
| Explicit independent add-on exception | Corrected in this audit | Trials & Add-ons |
| Perpetual base + subscription add-on | Covered | Trials & Add-ons |
| Dynamic generic constraint model | Covered | Policy Model |
| Pooled quantity redistribution | Covered | Entitlements |
| Transactional reallocation / supersession | Covered | Entitlements, Indexing & Concurrency |
| Multi-site device assignments | Covered | Backend Schema / Product |
| Per-site feature limits on one device | Corrected in this audit | Entitlements |
| Trial default 7 days | Covered | Trials & Add-ons |
| Trial starts at first successful activation | Covered | Trials & Add-ons |
| One trial per customer entitlement + feature baseline | Corrected in this audit | Trials & Add-ons |
| Admin/campaign trial override | Covered | Trials & Add-ons, Approval Workflows |
| No globally reusable trial license | Corrected in this audit | Business Rules / Trials |
| Commercial expiry, offline freshness, grace separate | Covered | Renewal |
| Check-in does not extend commercial term | Covered | Renewal |
| Payment alone does not renew offline device | Covered | Renewal |
| Renewal reminder baseline 30/7/1 | Corrected in this audit | Renewal / Notifications |
| Renewal lifecycle issued/delivered/accepted distinction | Corrected in this audit | Renewal / Portal IA |
| Grace/restricted state preserves recovery/diagnostics where safe | Corrected in this audit | Renewal / Device Lifecycle |
| Revocation online vs air-gapped behavior | Covered | Device Lifecycle / Offline |
| Device transfer approval/audit | Corrected in this audit | Device Lifecycle |
| Replacement/decommission returns allocation | Corrected in this audit | Device Lifecycle |
| Rehost after major identity change | Covered | Device Identity |

## Device identity and trust

| Requirement | Status | Handbook location |
|---|---|---|
| Device key + weighted/versioned fingerprint | Covered | Device Identity |
| MAC only supporting evidence | Covered | Device Identity / Threat Model |
| Short-lived single-use enrollment authorization | Covered | Backend Modules / Threat Model |
| Minor hardware change tolerance | Covered | Device Identity |
| Motherboard/key change => REHOST_REQUIRED | Covered | Device Identity |
| Clock rollback detection and restriction/revalidation | Corrected in this audit | Threat Model |
| Monotonic grant revision anti-rollback | Covered | Grant Format / Threat Model |

## Capacity

| Requirement | Status | Handbook location |
|---|---|---|
| Stable inventory separate from dynamic snapshots | Covered | Capacity Inventory |
| Detailed CPU/RAM/GPU/storage/runtime/camera fields | Corrected in this audit | Capacity Inventory |
| Benchmark-profile based planning | Covered | Capacity Inventory |
| Combined existing + proposed workload assessment | Covered | Capacity Planning |
| Central advisory vs local authoritative capacity | Corrected/strengthened | Capacity Authority |
| Rights never silently reduced by capacity | Covered | Capacity |
| Recommendation mode; customer/admin chooses | Corrected/strengthened | Capacity Authority |
| Example alternatives such as fewer cameras/FPS/hardware | Covered | Capacity Authority |

## Marketplace and portal

| Requirement | Status | Handbook location |
|---|---|---|
| Marketplace inside LMS logical modules | Covered | ADR-003 |
| Discover / trial / buy flow | Covered | Marketplace, Sequences |
| Customer feature details: description, release, compatibility, capacity, entitlement, trial, purchase | Corrected in this audit | Portal Information Architecture |
| Admin catalog: product/OS/hardware/dependencies/trial/commercial/release/campaign | Corrected in this audit | Portal Information Architecture |
| Corporate primary navigation | Corrected in this audit | Portal Information Architecture |
| Marketplace action does not itself grant permission | Covered | Business Rules / Trial & Add-ons |

## Release, OTA and model lifecycle

| Requirement | Status | Handbook location |
|---|---|---|
| AUTO/MANUAL update mode | Covered | Deployment |
| Stable default for automatic updates | Covered | Release Management |
| Explicit LTS control | Covered | Release Approval SOP |
| Maintenance window 01:00-03:00 default | Covered | Deployment |
| Traditional edge releases; no Docker dependency | Covered | ADR-004 |
| Automated migration / health / rollback | Covered | Update Manager |
| Keep 2-3 known-good releases where possible | Covered | Release Set |
| Models first-class independent OTA | Covered | Model OTA |
| Model inventory prevents redundant download | Covered | Model OTA |
| Models encrypted and signed | Covered | Model OTA / Model Protection |
| Device-authorized content-key use, no universal password | Covered | Model Protection / ADR-009 |
| App + model coordinated release-set rollback | Covered | Release Set |
| PostgreSQL metadata only; object/file repository for large artifacts | Corrected in this audit | Artifact Storage |
| SaaS S3-compatible / on-prem MinIO or approved repository abstraction | Corrected in this audit | Artifact Storage |
| Linux first, Windows-compatible future handlers | Covered | ADR-004 / Product Decisions |

## Offline / air-gapped

| Requirement | Status | Handbook location |
|---|---|---|
| Online, assisted offline, fully air-gapped | Covered | Deployment Models |
| Same signed trust model across routes | Covered | Trust Boundaries |
| Relay transport-only; no signing key | Covered | Trust Boundaries |
| Relay short-lived auth / encrypted staged storage | Corrected in this audit | Relay Security |
| Request ID + nonce + device binding | Covered | Offline Workflows |
| Minimal delta bundle when device already has artifact/model | Covered | Offline Workflows |
| Signed installation receipt and later reconciliation | Covered | Offline Workflows |
| Offline revocation delay explicitly acknowledged | Covered | Offline / Threat Model |

## Security and governance

| Requirement | Status | Handbook location |
|---|---|---|
| Separate license and release signing keys | Covered | ADR-006 |
| KMS/HSM/equivalent protected production custody | Covered | Signing |
| Root-compromised edge limitation acknowledged | Corrected/strengthened | Threat Model |
| Tenant isolation controls and negative tests | Covered | Tenant Isolation |
| Replay, rollback, cloning, clock, transfer, signing compromise threats | Covered | Threat Model |
| VAPT before production | Covered | VAPT / Release Readiness |
| Maker-checker for high-risk actions | Covered | Approval Workflows |
| Full role catalogue | Covered | RBAC |
| Audit retention 1-3 years configurable | Covered | Product Decisions / Audit |
| Backup/recovery with signing-key recovery separated | Covered | Backup & Recovery |
| Portal + email now; webhook extensibility | Covered | Notifications |

## Required state machines

| State machine | Status |
|---|---|
| Device | Covered |
| Grant/license | Covered |
| Trial | Corrected in this audit |
| Purchase request | Corrected in this audit |
| Offline request/response | Corrected in this audit |
| Installation | Covered/expanded |
| Renewal | Corrected in this audit |
| Deployment job/target | Covered |

## Required sequences

| Sequence | Status |
|---|---|
| First-time registration | Covered |
| Base activation | Covered |
| Online trial | Corrected in this audit |
| Offline trial | Corrected in this audit |
| Feature purchase | Corrected in this audit |
| Add-on activation | Corrected in this audit |
| Capacity reassessment | Corrected in this audit |
| Online software/model update | Corrected in this audit |
| Offline software/model update | Corrected in this audit |
| Subscription/offline renewal | Covered |
| Replacement/rehost | Corrected in this audit |
| Transfer | Corrected in this audit |
| Revocation | Corrected in this audit |
| Failed rollback | Corrected in this audit |
| Check-in freshness expiry | Corrected in this audit |
| Commercial expiry/grace | Corrected in this audit |

## Team and delivery governance

| Requirement | Status | Handbook location |
|---|---|---|
| Backend responsibilities | Covered |
| Edge/application responsibilities | Covered |
| AI/ML performance responsibilities | Covered |
| DevOps/security responsibilities | Covered |
| Product/commercial/QA policy ownership | Corrected/expanded | RACI |
| Delivery phases | Covered |
| Definition of Ready/Done | Covered |
| Release-readiness checklist | Covered |
| Git/PR/change control | Covered |
| Support escalation/runbooks | Covered |

## Remaining intentional open decisions

These are documented and should not be invented prematurely:

1. Production human authentication / OIDC / SSO / MFA profile.
2. Exact model content-key wrapping, secure local key storage and rotation profile.
3. Final release archive/package format and script execution constraints.
4. Telemetry privacy, opt-in/opt-out, retention and data residency.
5. Enterprise HA topology and contractual RTO/RPO.
6. Final API schemas/error catalog freeze after implementation review.
7. Product-specific benchmark matrix and performance thresholds.
8. Final support window for historical application versions.

## Audit conclusion

The handbook previously had real omissions in lifecycle state machines, required sequences, portal information architecture, trial eligibility, renewal milestones, device transfer/replacement, relay security, capacity authority, detailed inventory, artifact storage and several security threat details.

Those gaps are now explicitly documented.

Future handbook reviews should use this page as a regression checklist: if a design changes one of these requirements, the corresponding detailed page and this audit must be updated in the same PR.
