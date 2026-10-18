# Release Approval SOP

This SOP governs promotion into production-capable channels.

## Roles

- Developer: produces Development/QA artifacts
- QA: validates functional/integration/regression evidence
- Security: validates security gates for applicable changes
- Release Manager: owns promotion and rollout
- Product/Architecture: approves material compatibility/policy impact when needed

## Promotion path

~~~text
Development -> QA -> Internal/Beta -> Stable -> LTS (explicit)
~~~

## Stable promotion evidence

The promotion record references:
- source commit/tag
- build identity
- signed release manifest
- automated test report
- upgrade/migration test
- rollback test
- compatibility matrix
- capacity/benchmark impact if relevant
- security scan/VAPT disposition
- release notes
- known issues and rollback trigger

## Decision

Stable promotion uses maker-checker: Release Manager requests; required QA/Security approver confirms evidence. Same actor must not self-approve when policy requires separation.

## LTS

LTS is never automatic. Company explicitly designates an eligible Stable release as LTS after stability evidence and support-life decision.

## Emergency release

Emergency releases may use an expedited path but still require source traceability, approval, signed artifacts, rollback plan and post-release review within the defined incident process.