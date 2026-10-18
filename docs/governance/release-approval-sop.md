# Release Approval SOP

This SOP governs promotion into production-capable channels. Promotion approves an exact immutable release identity and evidence set, not merely a version label.

## Roles

- **Developer** — produces source/change and Development/QA candidates
- **QA** — validates functional/integration/regression/upgrade/rollback evidence
- **Security** — validates security gates/findings for affected scope
- **Release Manager** — owns promotion, rollout strategy and stop/rollback decision
- **Product/Architecture** — approves material policy/compatibility/architecture impact
- **Operations** — validates monitoring/runbook/deployment readiness where required

## Promotion path
~~~text
Development -> QA -> Internal/Beta -> Stable -> LTS (explicit)
~~~

Artifacts/manifests are immutable; promotion changes release eligibility/channel metadata, not the artifact bytes.

## Stable promotion evidence

Promotion record links:
- source commit/tag
- CI build/run identity
- signed release manifest + artifact hashes
- SBOM/provenance
- unit/integration/contract results
- supported-version upgrade/migration result
- rollback result
- compatibility matrix
- representative hardware/capacity evidence where relevant
- security scan + VAPT disposition
- release notes/known issues
- rollout/canary/concurrency plan
- automatic stop/rollback triggers
- operations/runbook impact

## Approval

Stable promotion uses maker-checker. Release Manager submits; required QA/Security/domain approvers review the same release/artifact hash/revision. Material artifact/evidence change invalidates approval.

## Rollout

Promotion to Stable does not require immediate deployment to all devices. Deployment policy may use pilot/canary/batches and halt on systemic failure threshold.

## LTS

LTS is never automatic. It requires an eligible Stable release plus explicit support-life decision, upgrade path, known-issue/security posture review and operational commitment.

## Emergency release

Emergency path may compress timing but retains:
1. source/build traceability
2. security/technical approver
3. immutable signed artifacts
4. focused validation
5. rollback/containment plan
6. incident/change reference
7. post-release full review

## Revocation/retirement

A bad/vulnerable release may be blocked/retired from new deployment. Existing installed devices follow controlled rollback/update policy; release metadata is not deleted to hide history.

## Evidence retention

Promotion/approval records remain auditable for the release support/audit period.