# System Design Requirements (SDR)

This section is the normative, testable design-requirement baseline for LMS. It converts the architecture and business rules into uniquely identified requirements that engineering, QA, security and operations can trace to implementation and acceptance evidence.

## Requirement language

- **SHALL** = mandatory requirement.
- **SHOULD** = expected unless an approved exception exists.
- **MAY** = optional capability.
- Every SHALL requirement must be traceable to implementation and verification evidence before production release.

## 1. Platform and deployment requirements

| ID | Requirement | Verification |
|---|---|---|
| SDR-PLT-001 | LMS SHALL provide one reusable control plane for current and future enterprise AI products. | architecture review + product onboarding test |
| SDR-PLT-002 | SaaS and customer-hosted LMS SHALL use the same core domain/application codebase except for deployment/provider adapters. | code/config review |
| SDR-PLT-003 | The central backend SHALL begin as a modular monolith with explicit bounded modules rather than mandatory microservices. | architecture review |
| SDR-PLT-004 | Edge application releases SHALL not require Docker as the runtime packaging dependency. | package/install test |
| SDR-PLT-005 | Linux SHALL be supported first while edge abstractions SHALL preserve a future Windows implementation path. | interface/package review |
| SDR-PLT-006 | LMS SHALL support online, assisted-offline and fully air-gapped device operations. | end-to-end tests |
| SDR-PLT-007 | Customer-hosted LMS upgrades SHALL be supported using a signed/manual package process in the initial release. | upgrade test |

## 2. Customer, site and device requirements

| ID | Requirement | Verification |
|---|---|---|
| SDR-DEV-001 | LMS SHALL model Customer, Site and Device as separate identities with immutable IDs. | schema/API test |
| SDR-DEV-002 | A device SHALL have one commercial customer owner at a time. | DB constraint/service test |
| SDR-DEV-003 | A device MAY serve multiple sites through explicit device-site assignments. | topology test |
| SDR-DEV-004 | Device registration SHALL be independent from commercial licensing and capacity validation. | state/API test |
| SDR-DEV-005 | Device identity SHALL use a device-generated asymmetric key plus a versioned hardware fingerprint. | enrollment test |
| SDR-DEV-006 | MAC/network addresses SHALL be supporting evidence only and SHALL NOT be the primary identity. | security review/test |
| SDR-DEV-007 | Enrollment authorizations SHALL be high-entropy, short-lived and single-use. | negative/security test |
| SDR-DEV-008 | Minor hardware changes SHALL trigger re-evaluation without mandatory rehost when identity remains within tolerance. | hardware-change test |
| SDR-DEV-009 | Major identity changes such as motherboard replacement or device-key loss SHALL enter REHOST_REQUIRED. | rehost test |
| SDR-DEV-010 | Device transfer SHALL be explicit, authorized and auditable; ownership SHALL NOT be silently overwritten. | transfer workflow test |
| SDR-DEV-011 | Decommission/replacement SHALL return or reconcile eligible allocations before final retirement. | lifecycle test |

## 3. Entitlement, allocation and grant requirements

| ID | Requirement | Verification |
|---|---|---|
| SDR-LIC-001 | LMS SHALL distinguish Entitlement, Allocation and Grant. | domain/schema review |
| SDR-LIC-002 | Entitlement SHALL represent customer-owned commercial rights. | domain/API test |
| SDR-LIC-003 | Allocation SHALL distribute pooled rights to device/site scope without exceeding approved entitlement quantity. | transactional concurrency test |
| SDR-LIC-004 | Grant SHALL be the signed executable authorization bound to a device. | grant verification test |
| SDR-LIC-005 | Commercial rights SHALL NOT be encoded as product-specific boolean columns such as `ppe_enabled`. | schema review |
| SDR-LIC-006 | Dynamic constraints SHALL support quantity, site, model/runtime and dependency restrictions. | policy/grant tests |
| SDR-LIC-007 | Replacement grants SHALL use revision and supersession semantics. | anti-rollback test |
| SDR-LIC-008 | Devices SHALL reject older grant revisions in an accepted grant lineage unless an explicitly signed recovery mechanism permits otherwise. | rollback attack test |
| SDR-LIC-009 | Subscription and perpetual base entitlements SHALL both be representable without schema redesign. | model/API test |
| SDR-LIC-010 | Perpetual licenses SHALL support explicit update-right policies. | policy test |
| SDR-LIC-011 | A device serving multiple sites SHALL be able to receive device-bound grants containing site-specific limits. | multi-site grant test |

## 4. Trial and add-on requirements

| ID | Requirement | Verification |
|---|---|---|
| SDR-TRL-001 | Default trial duration SHALL be 7 days and SHALL be policy configurable. | policy test |
| SDR-TRL-002 | Trial time SHALL begin at first successful feature activation, not at request, issuance or package import. | lifecycle test |
| SDR-TRL-003 | Baseline eligibility SHALL permit one trial per customer entitlement + feature unless an approved policy/campaign override exists. | eligibility test |
| SDR-TRL-004 | Trials SHALL be implemented as signed time-limited grants. | grant test |
| SDR-TRL-005 | Globally reusable trial licenses SHALL be prohibited. | security review |
| SDR-ADD-001 | Subscription add-ons SHALL co-terminate with the active base subscription by default. | term-calculation test |
| SDR-ADD-002 | Product/commercial policy MAY define explicitly independent add-ons with separate terms. | policy test |
| SDR-ADD-003 | A perpetual base SHALL support subscription add-ons. | lifecycle test |
| SDR-ADD-004 | A dependent add-on SHALL become dormant when its required base is inactive unless explicitly independent. | dependency test |

## 5. Time, renewal and revocation requirements

| ID | Requirement | Verification |
|---|---|---|
| SDR-LIF-001 | Commercial expiry, offline authorization freshness and grace SHALL be independent clocks. | time-state tests |
| SDR-LIF-002 | Default offline authorization freshness SHALL be 7 days unless policy overrides it. | policy test |
| SDR-LIF-003 | Default grace SHALL be 7 days unless separately overridden. | policy test |
| SDR-LIF-004 | A successful check-in SHALL NOT extend the paid commercial term. | renewal/check-in test |
| SDR-LIF-005 | Payment/central renewal SHALL NOT activate an offline device until a new signed grant revision is delivered/imported and accepted. | offline renewal test |
| SDR-LIF-006 | Renewal state SHALL distinguish requested, approved/issued, delivered/imported and accepted/active. | state-machine test |
| SDR-LIF-007 | Connected revocation SHALL be delivered through sync/check-in according to policy. | online revoke test |
| SDR-LIF-008 | Air-gapped revocation SHALL take effect only when new signed state is imported or current offline authorization expires. | air-gap test |
| SDR-LIF-009 | Grace/restricted state SHOULD preserve diagnostics, license recovery/import and existing-data access where safe. | product acceptance test |

## 6. Capacity requirements

| ID | Requirement | Verification |
|---|---|---|
| SDR-CAP-001 | Licensed, Compatible, Capacity Validated and Installed/Healthy SHALL be separate states. | API/UI/state test |
| SDR-CAP-002 | Stable hardware inventory SHALL be stored separately from dynamic resource snapshots. | schema test |
| SDR-CAP-003 | Capacity SHALL be evaluated from combined existing + proposed workload, not licensed quantity alone. | capacity regression test |
| SDR-CAP-004 | Workload definition SHALL include relevant camera/input, model, runtime, resolution, FPS, codec, decode and concurrency dimensions. | workload-schema test |
| SDR-CAP-005 | Capacity decisions SHALL be based on versioned benchmark evidence. | benchmark test |
| SDR-CAP-006 | Central capacity result SHALL be advisory/pre-assessment. | service contract test |
| SDR-CAP-007 | Local Capacity Engine SHALL be authoritative for actual feature activation. | edge activation test |
| SDR-CAP-008 | Capacity failure SHALL NOT silently reduce purchased entitlement. | negative business-rule test |
| SDR-CAP-009 | Capacity Engine SHALL return explicit alternatives/recommendations when selected workload does not meet target. | recommendation test |
| SDR-CAP-010 | Operator/customer SHALL explicitly select an allowed reduced configuration; LMS SHALL record that selection. | audit/workflow test |
| SDR-CAP-011 | Capacity assessment SHALL become stale when material hardware/runtime/model/workload/benchmark inputs change. | reassessment test |

## 7. Marketplace requirements

| ID | Requirement | Verification |
|---|---|---|
| SDR-MKT-001 | Marketplace SHALL be integrated into LMS while remaining a distinct logical module. | architecture review |
| SDR-MKT-002 | Marketplace SHALL support discover, trial and purchase-request flows. | UI/API E2E test |
| SDR-MKT-003 | Catalog discovery/trial/purchase state SHALL NOT itself authorize runtime execution. | authorization test |
| SDR-MKT-004 | Feature detail SHALL expose description, release/version, compatibility, capacity preview, entitlement state, trial status, purchase action and dependencies. | portal acceptance test |
| SDR-MKT-005 | Admin catalog SHALL support product/OS/architecture/runtime/hardware/dependency/model/trial/commercial/release visibility metadata. | admin acceptance test |

## 8. Release and OTA requirements

| ID | Requirement | Verification |
|---|---|---|
| SDR-OTA-001 | Release channels SHALL include non-production stages plus Stable, LTS and Retired semantics. | release-state test |
| SDR-OTA-002 | Automatic production OTA SHALL consume Stable by default. | policy test |
| SDR-OTA-003 | LTS SHALL be explicitly designated and SHALL NOT be automatic. | approval test |
| SDR-OTA-004 | AUTO and MANUAL deployment modes SHALL be supported. | deployment test |
| SDR-OTA-005 | Default automatic maintenance window SHALL be 01:00–03:00 in site timezone and SHALL be configurable. | scheduling test |
| SDR-OTA-006 | Release manifests and artifacts SHALL be signed/hashed and immutable after publication. | artifact-integrity test |
| SDR-OTA-007 | Normal releases SHALL automate migrations/install/health-check and SHALL NOT require manual site migration. | upgrade test |
| SDR-OTA-008 | Update Manager SHALL preserve at least the immediately previous known-good release set. | rollback test |
| SDR-OTA-009 | Failed health check SHALL cause coherent release-set rollback. | failure-injection test |
| SDR-OTA-010 | OTA SHALL support delta/minimal artifact transfer where content is already present and verified. | download/import test |
| SDR-OTA-011 | PostgreSQL SHALL store release metadata, not large application/model binaries. | storage review |

## 9. Model OTA requirements

| ID | Requirement | Verification |
|---|---|---|
| SDR-MOD-001 | AI models SHALL be independently versioned first-class OTA artifacts. | model lifecycle test |
| SDR-MOD-002 | Model artifacts SHALL be encrypted and signed. | crypto/artifact test |
| SDR-MOD-003 | Model inventory SHALL prevent unnecessary re-download of an already-present verified version. | delta test |
| SDR-MOD-004 | A universal embedded model password/customer-wide static decryption secret SHALL be prohibited. | security review |
| SDR-MOD-005 | Model use SHALL require entitlement authorization plus device/deployment-authorized content-key handling. | security integration test |
| SDR-MOD-006 | Model-only update SHALL be supported when compatibility constraints pass. | deployment test |
| SDR-MOD-007 | Application/plugin/UI/runtime/model versions SHALL be composable into a coherent Release Set for coordinated rollback. | release-set test |

## 10. Offline and air-gapped requirements

| ID | Requirement | Verification |
|---|---|---|
| SDR-OFF-001 | Offline request SHALL contain request ID, nonce, device identity reference, current revisions/inventory and requested operation. | schema test |
| SDR-OFF-002 | Device SHALL sign the canonical offline request. | signature test |
| SDR-OFF-003 | Central LMS SHALL validate tenant/device ownership, enrollment, eligibility, request age and anti-replay before issuing a response. | negative test |
| SDR-OFF-004 | Response SHALL be bound to request ID, nonce and target device. | wrong-device/replay test |
| SDR-OFF-005 | Relay SHALL be transport-only and SHALL NOT possess signing authority. | architecture/security test |
| SDR-OFF-006 | Offline package parsing SHALL be bounded, quarantined and resistant to traversal/archive attacks. | fuzz/security test |
| SDR-OFF-007 | Device SHALL verify signature/hash/binding/revision/dependencies before activation/install. | import test |
| SDR-OFF-008 | Device SHALL generate a signed receipt for accepted activation/install. | receipt test |
| SDR-OFF-009 | Central LMS SHALL reconcile returned receipts later without assuming issuance equals acceptance. | reconciliation test |

## 11. Backend and data requirements

| ID | Requirement | Verification |
|---|---|---|
| SDR-BE-001 | Backend baseline SHALL use Python 3.12 + FastAPI + PostgreSQL + SQLAlchemy + Alembic + Pydantic unless superseded by ADR. | architecture/build review |
| SDR-BE-002 | Schema migrations SHALL use Alembic; ad-hoc production SQL SHALL NOT be the standard deployment path. | CI/release review |
| SDR-BE-003 | Commercially atomic workflows SHALL use database transactions and optimistic concurrency where appropriate. | transaction tests |
| SDR-BE-004 | External side effects SHALL use durable outbox/job patterns when they cannot join the DB transaction. | failure/restart test |
| SDR-BE-005 | Retryable write workflows SHALL support idempotency. | duplicate-request test |
| SDR-BE-006 | API errors SHALL use stable machine-readable codes and safe messages. | contract test |
| SDR-BE-007 | Collections SHALL be bounded/paginated. | API test |
| SDR-BE-008 | Long-running operations SHALL expose durable job/resource state rather than depend on one long HTTP request. | job test |
| SDR-BE-009 | All tenant data access SHALL validate customer/tenant scope server-side. | isolation test |

## 12. Portal requirements

| ID | Requirement | Verification |
|---|---|---|
| SDR-UI-001 | Portal SHALL provide role/scoped views for vendor, release, security, customer, site, support and read-only personas. | UX/RBAC acceptance |
| SDR-UI-002 | Device view SHALL show registration, license/grant, expiry/offline/grace, capacity, release/model inventory, site assignments and deployment state separately. | UI acceptance |
| SDR-UI-003 | Renewal UI SHALL distinguish issued, delivered/imported and accepted/active. | UI state test |
| SDR-UI-004 | Capacity UI SHALL display purchased rights separately from selected active configuration. | UI acceptance |
| SDR-UI-005 | Privileged actions SHALL show approval state and SHALL NOT execute solely because UI control is visible. | security/UI test |

## 13. Security requirements

| ID | Requirement | Verification |
|---|---|---|
| SDR-SEC-001 | Human authorization SHALL be deny-by-default and scoped by permission plus object/customer context. | authz tests |
| SDR-SEC-002 | Production privileged human access SHALL target enterprise OIDC/SSO with MFA where supported by the chosen IdP. | security acceptance |
| SDR-SEC-003 | License-signing and release-signing keys SHALL use separate key purposes. | KMS/signing test |
| SDR-SEC-004 | Production signing private keys SHALL remain in KMS/HSM/equivalent protected provider and SHALL NOT be stored in LMS DB/config. | key-custody review |
| SDR-SEC-005 | Production secrets SHALL come from approved secret-management/deployment mechanisms and SHALL NOT be committed to source. | secret scan/config review |
| SDR-SEC-006 | TLS/certificate validation SHALL NOT be disabled in production. | deployment test |
| SDR-SEC-007 | Cross-tenant read/write SHALL be treated as a release-blocking security defect. | tenant negative tests |
| SDR-SEC-008 | Privileged/high-risk operations SHALL be audited; defined actions SHALL use maker-checker. | approval/audit tests |
| SDR-SEC-009 | Supply-chain controls SHALL include code review, SAST/SCA/secret scan, SBOM/provenance and signed release artifacts. | CI/release evidence |
| SDR-SEC-010 | Security logs SHALL capture sensitive administrative/security events without recording secret/key material. | logging tests |
| SDR-SEC-011 | VAPT SHALL cover auth, tenant isolation, enrollment, signing, offline parser, OTA, replay/rollback and transfer/rehost surfaces. | VAPT scope review |
| SDR-SEC-012 | Software-only edge security SHALL NOT claim complete protection against persistent root/administrator compromise. | architecture review |

## 14. Audit, notification and telemetry requirements

| ID | Requirement | Verification |
|---|---|---|
| SDR-AUD-001 | Privileged and business-significant mutations SHALL generate append-only audit events. | audit test |
| SDR-AUD-002 | Audit retention baseline SHALL support configurable 1–3 years. | retention test/config review |
| SDR-NOT-001 | Portal and email SHALL be initial notification channels. | notification test |
| SDR-NOT-002 | Notification design SHALL permit future webhook adapters without rewriting business modules. | architecture review |
| SDR-TEL-001 | High-volume telemetry SHALL be logically separated from transactional licensing data. | architecture/storage test |
| SDR-TEL-002 | Licensing SHALL NOT depend on successful delivery of best-effort high-volume telemetry. | outage test |
| SDR-TEL-003 | Telemetry SHALL support bounded offline buffering, retry and deduplication. | telemetry delivery test |

## 15. Operations and recovery requirements

| ID | Requirement | Verification |
|---|---|---|
| SDR-OPS-001 | PostgreSQL, audit state, artifact metadata and artifact binaries SHALL have protected backup/recovery mechanisms. | restore exercise |
| SDR-OPS-002 | Signing private-key recovery SHALL be separate from ordinary application/database backups. | DR review/exercise |
| SDR-OPS-003 | Backup reliability SHALL be proven through scheduled restore exercises. | restore evidence |
| SDR-OPS-004 | Production monitoring SHALL cover API, DB, signing, artifact storage, jobs/outbox, deployment, check-in/renewal, capacity and backup state. | monitoring acceptance |
| SDR-OPS-005 | Runbooks SHALL exist for API/DB/signing/artifact failure, bad rollout/rollback, offline rejection, rehost, allocation conflict, key compromise, restore and ERP mismatch. | runbook review/exercise |
| SDR-OPS-006 | Customer-hosted upgrade SHALL validate source version, signed package, backup, migration, health and rollback/forward-recovery constraints. | upgrade acceptance |

## 16. QA and release requirements

| ID | Requirement | Verification |
|---|---|---|
| SDR-QA-001 | CI SHALL include unit/integration/contract/security tests appropriate to the changed trust boundary. | CI review |
| SDR-QA-002 | Tenant-isolation tests SHALL be release blocking. | CI policy |
| SDR-QA-003 | OTA releases SHALL test upgrade, health check and rollback from supported source versions. | release evidence |
| SDR-QA-004 | Critical offline flows SHALL be tested end-to-end including wrong device, replay, stale revision and corrupted package. | system tests |
| SDR-QA-005 | Representative hardware SHALL be used for capacity/update tests. | lab evidence |
| SDR-QA-006 | Performance/load/soak/resilience tests SHALL be run before production readiness for critical workflows. | performance report |
| SDR-QA-007 | Stable/LTS release SHALL require traceable QA/security/release approval evidence. | release approval record |

## 17. Integration requirements

| ID | Requirement | Verification |
|---|---|---|
| SDR-INT-001 | ERP SHALL remain separate from LMS. | architecture review |
| SDR-INT-002 | ERP SHALL own invoice/payment/order truth where integrated; LMS SHALL own operational entitlement/allocation/grant state. | integration test |
| SDR-INT-003 | ERP inbound events SHALL be idempotent and unknown SKU mappings SHALL be quarantined for review. | integration test |
| SDR-INT-004 | ERP/commercial approval SHALL NOT directly mutate a device grant without LMS entitlement/policy processing. | workflow test |
| SDR-INT-005 | Reconciliation SHALL surface missing/extra/quantity/term/mapping mismatches without destructive auto-correction. | reconciliation test |

## 18. Traceability and design-governance requirements

| ID | Requirement | Verification |
|---|---|---|
| SDR-GOV-001 | Material behavior, API, schema, security-boundary or operational changes SHALL update handbook/ADR in the same PR. | PR review |
| SDR-GOV-002 | Architecture/security/commercial-policy changes SHALL use the documented approval path. | governance audit |
| SDR-GOV-003 | Every mandatory SDR requirement SHALL map to one or more implementation work items and acceptance tests before production. | traceability review |
| SDR-GOV-004 | Open decisions SHALL remain explicit and SHALL NOT be silently resolved by implementation defaults. | ADR/release review |

## 19. Open decisions that constrain SDR implementation

The following are deliberately not frozen by this SDR yet: production OIDC/SSO provider/profile; exact model content-key wrapping and edge secure storage; final edge release archive format; product/hardware-specific benchmark thresholds; telemetry privacy/residency/retention policy; enterprise HA topology/RTO/RPO; final generated OpenAPI/physical DDL; historical-version support window.

Implementation SHALL preserve the documented abstraction until the owning decision is approved.

## 20. Requirement traceability template

Use this structure in implementation planning:

~~~text
SDR ID          : SDR-LIC-003
Design / ADR    : Entitlements & Allocations / relevant ADR
Implementation  : issue/epic/PR
Test            : automated test ID / test report
Release evidence: build/release link
Owner           : module/team
Status          : planned | implemented | verified | accepted
~~~

An SDR requirement is not considered verified merely because code exists; evidence must demonstrate the stated behavior.