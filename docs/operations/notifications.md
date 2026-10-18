# Notification Events & Templates

Phase 1 channels are portal + email. The event model must allow webhooks later without changing business modules.

## Notification event catalogue

| Event | Default audience | Urgency |
|---|---|---|
| renewal_due_30d | Customer Admin, Vendor account owner | normal |
| renewal_due_7d | Customer Admin, Vendor account owner | high |
| renewal_due_1d | Customer Admin, Vendor account owner | high |
| license_entered_grace | Customer Admin, Support | high |
| offline_checkin_stale | Customer Admin, Support | high |
| trial_expiring | Customer Admin | normal |
| trial_expired | Customer Admin | normal |
| deployment_scheduled | Customer/Site Admin | normal |
| deployment_failed | Customer/Site Admin, Support | high |
| rollback_completed | Support, Release Manager | high |
| device_rehost_required | Customer Admin, Support | high |
| entitlement_overallocation_attempt | Customer Admin, Support | normal |

## Template rules

Templates include customer/site/device display names, safe remediation steps and portal deep-link identifiers. They never include secrets, raw license payloads, private keys or decrypted model information.

## Delivery tracking

Persist notification ID, event ID, recipient, channel, template version, send attempt, result and delivered timestamp. Repeated transient failures retry with backoff; permanent failures are visible to operations.