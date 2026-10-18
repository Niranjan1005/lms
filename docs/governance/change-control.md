# Engineering Change Control

Change control provides traceability and proportionate review without turning every edit into the same process. The required controls depend on what business/security boundary a change affects.

## Change classes

| Class | Examples | Minimum controls |
|---|---|---|
| Standard | bug fix, docs correction, internal refactor | PR, tests, qualified review |
| Architecture | new module, trust boundary, persistence model, deployment topology | SDR/ADR impact review, architecture approval, PR/tests |
| Security-sensitive | auth/RBAC, signing, offline parser, model protection, secret handling | security review, negative tests, scan/VAPT scope review |
| Commercial-policy | entitlement, allocation, trial, renewal, expiry/grace, transfer | Product/Commercial approval, regression tests, audit impact |
| Release/OTA | manifest, package, migration, rollback, channel behavior | Release/Edge review, upgrade/rollback evidence |
| Data migration | destructive/backfill/tenant ownership changes | migration plan, backup/recovery, performance/locking review |
| Emergency | critical security/production correction | expedited approver path + full post-change review |

## Required traceability

A material production change is traceable through:
~~~text
Requirement / incident / issue
        ↓
SDR + ADR impact
        ↓
PR / review
        ↓
CI / security / test evidence
        ↓
Release identifier / manifest
        ↓
Deployment / migration / audit event
        ↓
Post-release validation
~~~

## Pre-change assessment

Every material PR identifies:
- affected customers/tenants/modules
- API/schema/state-machine impact
- security/trust boundary impact
- online/offline behavior
- migration/upgrade/rollback requirement
- capacity/model/release compatibility impact
- observability/runbook changes
- whether customer communication is required

## Approval separation

Requesters must not self-approve actions where maker-checker or security/release separation is mandated. Code review is not automatically equivalent to commercial/security approval.

## Emergency changes

Emergency does not mean uncontrolled. Minimum requirements are:
1. incident/change owner
2. scoped risk statement
3. at least one authorized approver appropriate to severity
4. test/smoke evidence practical for the emergency
5. rollback/containment plan
6. audit trail
7. post-change review and normal documentation/ADR update

## Prohibited changes

- direct untracked production DB edits as routine workflow
- bypassing signing/tenant authorization to restore service
- replacing published immutable release artifacts in place
- changing a commercial term/grant without auditable business workflow
- silently changing Approved ADR behavior inside an unrelated implementation PR

## Post-change validation

Validate release health, tenant isolation, audit events, migration correctness, deployment/rollback status and any affected operational alerts. Failed validation triggers rollback/forward recovery according to release plan.