# Git, Branching & Pull Request Standards

## Branching model

Use short-lived branches from `main`. `main` must remain releasable/documentation-buildable. Long-lived feature branches are discouraged.

Suggested naming:

~~~text
feature/<ticket>-short-name
fix/<ticket>-short-name
security/<ticket>-short-name
docs/<ticket>-short-name
~~~

## Pull request requirements

Every PR contains:
- problem/business context
- implementation summary
- affected modules
- API/schema/migration impact
- security impact
- test evidence
- rollback/compatibility notes where applicable
- documentation/ADR updates

## Review rules

At least one qualified reviewer for normal changes. Sensitive areas require an additional domain reviewer:
- authentication/RBAC/signing/offline parser -> Security
- entitlement/grant/policy -> Backend architecture/product owner
- release/update/model OTA -> Release/Edge owner
- DB migration -> Backend/data owner

## Merge policy

Prefer squash or rebase according to repository setting, but final history must retain ticket/PR traceability. Direct commits to protected `main` should be disabled once team development begins.

## Commit content policy

No secrets, private keys, customer exports, production credentials, decrypted model artifacts or proprietary binary releases should be committed to the documentation/source repository.