# Development Readiness Checklist

A work item is development-ready only when engineering can implement and test it without inventing missing product/security behavior during coding.

## Problem and scope

- [ ] business outcome and success metric defined
- [ ] in-scope and non-goal behavior written
- [ ] affected actors/personas identified
- [ ] affected SDR requirement IDs listed
- [ ] open decisions/ADRs identified

## State and business rules

- [ ] state machine/transition defined
- [ ] invariants defined
- [ ] success, warning, restricted and failure behavior defined
- [ ] online/offline/air-gapped behavior explicitly addressed where relevant
- [ ] retries/idempotency/concurrency behavior defined

## Data and API

- [ ] owning module identified
- [ ] DB aggregate/table ownership known
- [ ] transaction boundary known
- [ ] API/local interface/event contract drafted
- [ ] schema/version/backward-compatibility impact classified
- [ ] migration/backfill strategy defined if persistent data changes

## Security

- [ ] authentication principal identified
- [ ] authorization permission + scope defined
- [ ] tenant isolation behavior defined
- [ ] sensitive data classification identified
- [ ] signing/crypto/secrets impact reviewed
- [ ] abuse/replay/tamper cases identified
- [ ] maker-checker requirement evaluated

## Edge/capacity/release

- [ ] local enforcement boundary identified
- [ ] capacity impact assessed
- [ ] compatibility/release/model dependencies known
- [ ] upgrade/rollback behavior defined
- [ ] representative hardware/environment needs identified

## Operations

- [ ] required audit events identified
- [ ] logs/metrics/alerts identified
- [ ] failure/recovery/runbook impact identified
- [ ] external integrations and retry behavior identified

## QA

- [ ] acceptance criteria written
- [ ] happy/negative/security tests defined
- [ ] migration/upgrade/rollback tests defined where applicable
- [ ] offline and fault-injection tests defined where applicable
- [ ] test data/fixtures/environment available

## Ownership

- [ ] engineering owner
- [ ] product/business approver
- [ ] QA owner
- [ ] security/operations reviewer where risk requires it

If any mandatory item is unknown, the story remains discovery/design work rather than silently becoming an implementation assumption.