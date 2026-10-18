# Security Logging, Detection & Alerting

Security logging is separate from high-volume product telemetry. Security events must be durable enough for investigation and customer/tenant scoping.

## Required security event families

- login success/failure and lock/rate-limit events
- privileged role assignment/removal
- maker-checker request/approval/rejection
- enrollment authorization creation/use/replay failure
- device key registration/rehost/transfer
- grant issue/revoke/supersession/verification failure
- signing request/key rotation/trust-bundle change
- artifact/model signature/hash failure
- offline import rejection/replay/path/archive security failure
- tenant authorization denial and suspected cross-tenant access
- capacity/security override
- release Stable/LTS promotion and forced rollout
- secret/certificate rotation administrative actions
- audit export and sensitive report access

## Event fields

Security events record event type/version, UTC timestamp, request/correlation ID, actor principal/type, tenant/customer scope, source/device identifier where safe, target object, action/result, stable reason/error code and approval reference where relevant.

Secrets, raw bearer tokens, private keys, plaintext DEKs and decrypted models are prohibited from security logs.

## Detection examples

| Signal | Detection/alert intent |
|---|---|
| repeated enrollment-token failures | brute-force/abuse investigation |
| cross-tenant authorization denials spike | tenant isolation/security investigation |
| unknown signing key ID at devices | trust-bundle/deployment or compromise investigation |
| repeated offline replay rejection | operational misuse or malicious replay |
| signature/hash failures across fleet | artifact/signing/repository incident |
| privileged override volume anomaly | governance/security review |
| signing API denial/failure anomaly | signing-service incident |

## Retention and access

Security/audit retention follows configured policy with a baseline of 1–3 years. Access to global security logs is restricted and audited; customer-visible audit views are tenant-scoped.

## Time and integrity

Central systems use reliable time synchronization. Audit/security records are append-only at the application level; any archival/export pipeline preserves event identity and ordering metadata.

## Incident linkage

Alerts and incidents should carry request/event identifiers that allow responders to trace from portal/API action through business audit event, signing/deployment job and edge receipt without exposing sensitive payloads.