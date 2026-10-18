# Definition of Ready / Definition of Done

## Definition of Ready

A story/epic is Ready when:
- business outcome and acceptance criteria are written
- affected actors/scopes are known
- state transition is defined
- API/data ownership is identified
- authorization and tenant boundary are defined
- online/offline behaviour is explicit
- error/recovery path is documented
- security/capacity impact is classified
- dependencies and migration needs are known
- test approach is identified

## Definition of Done

A change is Done when:
- implementation is merged through review
- unit/integration/contract tests pass
- tenant authorization tests exist where applicable
- audit and observability are implemented
- DB/API compatibility and migration are validated
- upgrade and rollback are tested where applicable
- threat/security review is complete
- documentation and ADRs are updated in the same PR
- acceptance criteria are demonstrated
- no unresolved Sev-1/Sev-2 defects remain for release scope