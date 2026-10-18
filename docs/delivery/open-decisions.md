# Open Decisions

Open decisions are intentional unresolved choices. They must have an owner, decision deadline/milestone and constraints so implementation does not accidentally choose by default.

| Topic | Status | Must be decided before | Constraints already fixed |
|---|---|---|---|
| Production human authentication / OIDC / SSO / MFA profile | Open | production security freeze | RBAC/scope independent of IdP; privileged MFA target |
| Exact model key wrapping / secure local key storage | Security ADR required | production model OTA | no universal password; protected KMS/HSM boundary; device/deployment authorization |
| Telemetry privacy / opt-in / residency / retention | Open | production telemetry enablement | licensing cannot depend on high-volume telemetry |
| Final generated OpenAPI schemas/error catalogue freeze | Open | implementation/API freeze | `/v1`, stable error codes, idempotency/scoping rules |
| Enterprise HA topology and RTO/RPO | Open | enterprise SLA offering | Phase 1 backup/recovery required |
| Final release archive/package format | Proposed ADR | Update Manager implementation freeze | signed manifest/artifacts, traditional package, Windows-compatible abstraction |
| Benchmark thresholds/headroom per product/hardware | Product/performance decision | capacity production activation | benchmark profiles versioned; local authority |
| Supported historical-version upgrade window | Release/Support decision | first production upgrade policy | manifest declares supported source versions |

## Governance

Each open decision is resolved through ADR/product/operations approval appropriate to its domain. Until resolved, implementation must preserve the documented abstraction instead of hard-coding a choice.