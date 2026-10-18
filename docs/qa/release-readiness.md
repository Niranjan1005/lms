# Release Readiness

Release readiness is an evidence-based gate, not a checkbox ceremony. Stable/LTS promotion is allowed only when required evidence exists for the actual release scope and known exceptions are explicitly dispositioned.

## Required evidence

### Requirements and design
- affected SDR requirements identified
- ADR impact reviewed
- acceptance criteria approved
- breaking compatibility/migration impact documented
- known open decisions are not accidentally resolved by implementation

### Code and database
- code review complete
- static analysis/lint/type checks complete
- DB migrations reviewed and tested
- supported source-version upgrade path tested
- rollback or forward-recovery path tested
- destructive schema changes follow expand/contract policy

### Functional and integration
- unit tests green
- API/repository integration tests green
- central-edge contract tests green
- tenant-isolation negative tests green
- offline request/response and receipt flows tested when affected
- rehost/renewal/reallocation paths tested when affected

### Release and edge
- manifest/package hashes and signatures verified
- install/stage/migration/health flow tested
- coherent rollback tested
- model compatibility/warm-up tested where relevant
- capacity metadata/benchmark impact reviewed
- representative hardware validation completed for affected edge changes

### Security
- SAST/SCA/secret scan complete
- SBOM/provenance generated for production release
- security review completed for trust-boundary changes
- VAPT requirements satisfied or formally dispositioned
- signing/trust-store changes tested
- no unresolved prohibited-severity vulnerabilities for release policy

### Operations
- monitoring/alerts updated
- runbooks/support notes updated
- backup/restore impact reviewed
- deployment/rollback plan documented
- customer-hosted upgrade impact documented where applicable
- notification/reconciliation impacts tested

### Release governance
- release notes complete
- known issues listed
- rollout strategy/canary/concurrency defined
- automatic stop/rollback thresholds defined
- Stable/LTS approvals recorded
- source commit/build/release IDs traceable

## Blockers

A release SHALL NOT be promoted when any of these apply:
- failed tenant-isolation/security-critical test
- invalid/unverified signing or manifest integrity
- known data-loss migration without approved recovery
- rollback/recovery path absent for a risky deployment
- unresolved critical vulnerability without formal security acceptance
- unsupported source-version upgrade path is being targeted
- mandatory acceptance criteria not demonstrated

## Approval record

The promotion record links requirement/issue, PR/commit, build, test reports, security evidence, release manifest, SBOM/provenance, migration/rollback evidence and approvers.

## LTS additional gate

LTS additionally requires an explicit support-life decision, supported upgrade path, operational capacity and a commitment to maintain compatibility/security fixes for the declared window.