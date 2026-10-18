# Git, Branching & Pull Request Standards

Git/PR workflow provides review, traceability and release provenance. It must support security-sensitive domain ownership without creating long-lived branch divergence.

## Branching

Use short-lived branches from `main`:
~~~text
feature/<ticket>-short-name
fix/<ticket>-short-name
security/<ticket>-short-name
docs/<ticket>-short-name
release/<version>     # only if release process needs it
~~~

`main` remains releasable/buildable. Long-lived feature branches are discouraged.

## Pull request content

Every material PR contains:
- problem/business context
- affected SDR IDs
- ADR impact/new ADR if needed
- implementation summary
- affected modules
- API/event/local-interface impact
- DB/schema/migration impact
- tenant/security/privacy impact
- online/offline/edge behavior
- test evidence
- observability/runbook impact
- compatibility/upgrade/rollback notes
- documentation updates

## Review matrix

At least one qualified reviewer for normal changes. Additional review is required for:
- authentication/RBAC/tenant isolation/signing/offline parser/model keys -> Security
- entitlement/allocation/grant/renewal policy -> Backend + Product
- release/update/model OTA -> Release/Edge
- capacity/benchmark logic -> Performance/AI + Edge
- DB migration/concurrency -> Backend/Data
- operations/DR/deployment -> DevOps/Operations

## Approval versus code review

Code approval does not automatically satisfy maker-checker commercial/security actions. A PR may implement an approved workflow but does not itself approve a customer entitlement increase/key rotation/Stable promotion.

## CI requirements

PRs run applicable lint/type/unit/integration/security/migration/docs checks. Tenant-isolation/security-critical tests are release blockers. Docs-only changes run strict MkDocs build.

## Merge policy

Prefer squash/rebase according to repository setting, preserving ticket/PR traceability. Protected `main` should require PR review/status checks once team development begins; emergency bypass is auditable and reviewed afterward.

## Commit/repository content

Never commit passwords/tokens, private signing keys, model content keys, production credentials, raw sensitive customer exports, decrypted proprietary models or production binary release payloads not intended for source repository.

## Generated artifacts

Generated OpenAPI/schema/SBOM/provenance files may be committed or attached according to project convention, but the source that generates them and release linkage must be clear.

## Documentation

Behavior-changing PR updates SDR/domain docs in the same PR. Durable architecture change creates/supersedes ADR rather than burying rationale in PR comments.