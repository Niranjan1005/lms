# Engineering Decision Gates

Decision gates prevent unresolved product/security assumptions from moving invisibly into implementation and production. Evidence is linked to issues/PRs/test reports/releases rather than captured only in meetings.

## Gate 0 — Problem / Sponsor

Required outputs:
- business problem/outcome
- sponsor/product owner
- scope/non-goals
- success measures
- affected product/customer classes

Exit condition: problem is worth solving and scope is approved.

## Gate 1 — Architecture Ready

Required outputs:
- relevant SDR requirements
- system context/trust boundary impact
- state machine and invariants
- data ownership/transaction boundaries
- central/edge/offline behavior
- API/event/local interface draft
- ADR created/superseded for durable decisions
- threat/capacity/release implications

Exit condition: engineering is not expected to invent architecture while coding.

## Gate 2 — Development Ready

Required outputs:
- decomposed work items
- acceptance criteria
- owner/dependencies
- test approach
- migration/upgrade strategy
- environments/fixtures/hardware needed
- operational/audit/observability expectations

Exit condition: Definition of Ready satisfied.

## Gate 3 — Release Candidate

Required evidence:
- code review merged
- CI/integration/security tests
- schema migration result
- supported upgrade path
- rollback/recovery result
- tenant-isolation evidence
- package/manifest integrity
- capacity/model compatibility evidence where affected
- documentation current

Exit condition: build is technically eligible for production approval.

## Gate 4 — Production Approval

Required evidence:
- QA acceptance
- security/VAPT disposition
- release notes/known issues
- rollout/canary/concurrency plan
- stop/rollback triggers
- support/runbook readiness
- backup/recovery impact
- required maker-checker approvals

Exit condition: Stable promotion/deployment authorized.

## Gate 5 — Post-Release

Review:
- deployment/rollback health
- SLO/error/backlog signals
- customer/support incidents
- security anomalies
- unresolved follow-up items
- performance/capacity regressions
- whether release/ADR/runbook corrections are needed

Exit condition: release is accepted into normal operation or corrective actions are assigned.

## Gate ownership

Product owns problem/business gates; Architecture/Engineering owns design readiness; QA/Security/Release own production evidence; Operations owns recovery/monitoring readiness. High-risk changes require all relevant owners, not one blanket approver.