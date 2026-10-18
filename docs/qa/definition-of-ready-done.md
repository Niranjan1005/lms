# Definition of Ready / Definition of Done

Definition of Ready prevents incomplete design from becoming hidden implementation decisions. Definition of Done requires evidence that the change works, is secure, supportable and documented.

## Definition of Ready

A story/epic is Ready only when:
- business outcome and acceptance criteria are written
- affected SDR requirement IDs are identified
- affected actors/scopes are known
- state transition/invariants are defined
- owning module/data aggregate is identified
- API/event/local interface impact is drafted
- authorization and tenant boundary are defined
- online/offline/air-gapped behavior is explicit where relevant
- error/retry/idempotency/recovery behavior is documented
- security/privacy/capacity/release impact is classified
- dependencies and migration needs are known
- observability/audit/runbook impact is identified
- test environment/fixtures/hardware needs are available
- material ADR impact is resolved or explicitly open

If an item is unknown, the work remains discovery/design rather than being treated as implementation-ready.

## Definition of Done

A change is Done only when:
- implementation is merged through required review
- unit/integration/contract tests pass
- negative/security tests exist for changed trust boundaries
- tenant authorization tests pass where applicable
- DB/API/event compatibility is validated
- migration/backfill is tested with realistic data volume where applicable
- upgrade and rollback/forward-recovery are tested
- offline paths are tested if affected
- capacity/representative hardware tests are complete if affected
- audit events and observability are implemented
- support/runbook/error catalogue is updated when operational behavior changes
- security/threat review is completed
- SDR/ADR/handbook documentation is updated in the same PR
- acceptance criteria are demonstrated
- no unresolved release-blocking security/data-integrity defects remain

## Release Done versus Story Done

A merged story may be Done but not yet production-releasable. Stable/LTS promotion additionally requires release-readiness, packaging, full upgrade/rollback, security/VAPT and operational evidence.

## Exception handling

Any accepted exception records owner, risk, expiry/target remediation and approver. A vague 'follow up later' does not satisfy Done.