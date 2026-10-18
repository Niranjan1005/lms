# Support Escalation Model

Support escalation separates safe operational recovery from engineering/security decisions. Support must not bypass licensing, signing, tenant or release controls to make a symptom disappear.

## L1 — Operations / Support

Handles documented runbooks: customer/site/device lookup, entitlement/allocation/grant state, renewal delivery status, offline request/response validation, deployment receipt review, standard rehost coordination and known error-code remediation.

L1 MAY retry approved operational jobs, regenerate permitted offline responses from a fresh valid request, guide package import and collect diagnostics. L1 SHALL NOT hand-edit grants, modify DB commercial state, disable signature verification or use another tenant's data to troubleshoot.

## L2 — Engineering

Engaged when the issue indicates a reproducible software defect, migration/update problem, unexpected state transition, capacity anomaly, integration defect, performance regression or unsupported edge/runtime condition.

L2 owns code-level diagnosis, safe fixes, regression tests and release packaging. Production data changes require approved tooling/change procedure rather than ad-hoc SQL.

## L3 — Architecture / Security / Release

Engaged for signing/key incidents, tenant isolation suspicion, privilege/authentication failures, systemic Stable/LTS release failure, data-integrity risk, model-key compromise, cross-module design defects and emergency architecture decisions.

## Severity and target routing

| Example | Typical severity | Route |
|---|---|---|
| single device package rejected with known code | Sev-3/4 | L1 |
| multiple devices fail same migration | Sev-2 | L2 + Release |
| broad renewal/grant issuance outage | Sev-1/2 | L2/L3 + Operations |
| tenant data exposure suspicion | Sev-1 Security | L3 immediately |
| signing-key compromise suspicion | Sev-1 Security | L3 immediately |
| rollback also fails on production fleet | Sev-1/2 | L2/L3 |

## Escalation packet

Every escalation includes:
- customer/site/device identifiers
- request/correlation ID
- stable error code
- UTC timestamps + site timezone context
- entitlement/allocation/grant IDs and revisions
- release/model/release-set versions
- deployment/installation receipt state
- inventory/capacity assessment IDs where relevant
- safe relevant logs
- reproduction/steps already attempted
- customer/business impact
- whether issue is online/offline/air-gapped

Never send passwords, bearer tokens, signing/private keys, unwrapped model keys, decrypted models or unnecessary customer-sensitive payloads through ordinary support channels.

## Handoff and closure

Receiving level explicitly accepts ownership. Resolution records root cause, remediation, affected versions, workaround, permanent fix/release, tests added and whether runbook/error catalog/documentation must change.