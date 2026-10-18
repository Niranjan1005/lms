# Notification Events, Delivery & Templates

Notifications surface lifecycle events without becoming the source of truth. A failed email does not roll back renewal, grant issuance or deployment state.

## Initial channels

Phase 1 supports:
- portal/in-product notifications
- email

The event/delivery abstraction must allow future webhook or enterprise messaging adapters without changing business modules.

## Event catalogue
| Event | Default audience | Urgency | Typical trigger |
|---|---|---|---|
| renewal_due_30d | Customer Admin, account owner | normal | commercial expiry approaching |
| renewal_due_7d | Customer Admin, account owner | high | expiry approaching |
| renewal_due_1d | Customer Admin, account owner | high | imminent expiry |
| license_entered_grace | Customer Admin, Support | high | commercial/offline policy transition |
| offline_checkin_stale | Customer Admin, Support | high | freshness threshold |
| trial_expiring | Customer Admin | normal | trial clock nearing end |
| trial_expired | Customer Admin | normal | trial ended |
| deployment_scheduled | Customer/Site Admin | normal | target scheduled |
| deployment_failed | Customer/Site Admin, Support | high | install/health failure |
| rollback_completed | Support, Release Manager | high | automatic/manual rollback |
| rollback_failed | Support, Release Manager, Operations | critical | rollback health failure |
| device_rehost_required | Customer Admin, Support | high | major identity change |
| entitlement_overallocation_attempt | Customer Admin, Support | normal | rejected allocation |
| signing_service_degraded | Operations/Security | critical | signing outage |
| backup_failed | Operations | critical | backup job failure |

## Event generation

Business modules emit a notification request/event after committing relevant state. Notification delivery is asynchronous and idempotent; it must not participate in the commercial DB transaction.

## Recipient resolution

Recipient selection uses current scoped role/contact preferences and event customer/site context. Global operational/security alerts may use separate on-call routing rather than customer contacts.

## Template requirements

Templates include safe display names, relevant status, UTC/site-local time where helpful, stable support code, remediation guidance and portal deep-link identifier. They do not include passwords/tokens, private keys, raw grant payloads, unwrapped model keys or decrypted model content.

## Deduplication/throttling

Repeated state evaluation should not send duplicate reminders indefinitely. Notification keys include business event/object/window. High-volume failure alerts are grouped/throttled while preserving incident visibility.

## Delivery tracking

Persist notification/event ID, tenant, recipient, channel, template version, attempt count, status, provider reference and timestamps.

## Retry/failure

Transient provider failures retry with bounded backoff. Permanent address/provider failures are visible to operations/customer preference UI. Notification failure never marks the underlying renewal/deployment unsuccessful.

## Preferences

Customer/user preferences may control optional informational messages but cannot suppress mandatory security/critical operational notices where policy requires them.

## Related SDR

`SDR-NOT-001`, `SDR-NOT-002`, `SDR-OPS-004`