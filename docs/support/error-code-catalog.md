# Support Error Code Catalogue

Stable support codes allow customer support, logs and UI to refer to the same failure without exposing stack traces.

## Naming format

`LMS-<DOMAIN>-<HTTP>-<NNN>`

Examples:

| Code | Meaning | Operator action |
|---|---|---|
| LMS-AUTH-401-001 | Invalid credentials | Verify account; do not disclose which credential failed |
| LMS-DEVICE-409-001 | Device already registered to another active identity | Start transfer/rehost investigation |
| LMS-DEVICE-409-002 | Rehost required after major identity change | Submit rehost approval |
| LMS-ENT-409-001 | Entitlement pool over-allocation | Reduce requested allocation or increase approved entitlement |
| LMS-GRANT-409-001 | Stale grant revision | Fetch/import newest grant |
| LMS-GRANT-403-002 | Feature not entitled | Check entitlement/purchase state |
| LMS-OFFLINE-409-001 | Offline response does not match request nonce/device | Regenerate from fresh request |
| LMS-OFFLINE-409-002 | Offline package replay detected | Reject; investigate operator/process |
| LMS-CAP-422-001 | Workload incompatible with hardware | Review capacity recommendations |
| LMS-CAP-409-002 | Capacity assessment based on stale inventory | Refresh inventory and reassess |
| LMS-REL-422-001 | Release incompatible with OS/runtime | Select compatible release |
| LMS-REL-409-002 | Release blocked by dependency | Resolve required runtime/model |
| LMS-UPD-500-001 | Install failed; rollback completed | Inspect install logs and health-check failure |
| LMS-UPD-500-002 | Install failed; rollback also failed | Escalate Sev-2/Sev-1 based on scope |
| LMS-SIGN-503-001 | Signing service unavailable | Retry later; operations alert required |

## Support policy

UI shows the stable code and a customer-safe message. Secure logs retain request ID and technical context. Runbooks map critical codes to diagnostic steps.