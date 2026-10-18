# Deployment State Machine

Deployment uses separate job-level and target-level states. A fleet deployment can be partially successful; one device's failure must not erase the state/evidence of other targets.

## Job states
~~~text
DRAFT -> SCHEDULED -> RUNNING -> COMPLETED
            |           |          |
            |           |          +-> COMPLETED_WITH_FAILURES
            |           +-> PAUSED
            |           +-> CANCELLING -> CANCELLED
            +-> CANCELLED

RUNNING/PAUSED -> FAILED only for orchestration-level failure
~~~

## Target states
~~~text
PENDING
  -> WAITING_WINDOW
  -> PREFLIGHT
  -> DOWNLOADING / WAITING_OFFLINE_IMPORT
  -> VERIFYING
  -> STAGING
  -> INSTALLING
  -> HEALTH_CHECK
  -> ACTIVE

Any pre-commit state may -> FAILED
INSTALLING/HEALTH_CHECK may -> ROLLING_BACK -> ROLLED_BACK
ROLLING_BACK may -> ROLLBACK_FAILED
Eligible waiting states may -> CANCELLED
~~~

## State semantics
| State | Meaning |
|---|---|
| PENDING | target resolved but not yet eligible to execute |
| WAITING_WINDOW | waiting for maintenance/policy time |
| PREFLIGHT | license, compatibility, disk, dependency, capacity checks |
| DOWNLOADING | online artifact transfer |
| WAITING_OFFLINE_IMPORT | response package prepared/awaiting field import |
| VERIFYING | signed manifest/hash validation |
| STAGING | content prepared in non-active location |
| INSTALLING | migration/install handlers executing |
| HEALTH_CHECK | target services/model warm-up under validation |
| ACTIVE | atomic commit completed and health accepted |
| FAILED | target did not commit; reason recorded |
| ROLLED_BACK | failed/new release was reverted and previous set is healthy |
| ROLLBACK_FAILED | recovery failed; critical support/incident action required |

## Transition rules

- target cannot skip signature verification before install
- `ACTIVE` requires successful health check and commit
- download success alone is not installed/active
- cancellation after commit becomes a new rollback/deployment action, not history deletion
- retry creates attempt history; it does not erase previous failure evidence
- stale target eligibility is rechecked before install

## Fleet policy

Deployment job tracks batch/canary/concurrency and stop thresholds. Systemic signature/migration/rollback failure can PAUSE the remaining job automatically according to policy.

## Offline targets

Central may enter `WAITING_OFFLINE_IMPORT`/Delivered state after bundle generation, but target becomes Active only after signed installation receipt reconciliation.

## Audit/evidence

Every state transition records timestamp, actor/system, attempt, release set, policy snapshot, reason/error code and receipt where available.

## Related SDR

`SDR-OTA-004` through `SDR-OTA-010`