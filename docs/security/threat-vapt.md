# Threat Model & VAPT

| Threat | Baseline control |
|---|---|
| Token guessing | High entropy, short-lived/single-use token, rate limiting |
| Forged license | Protected signing key + signed grants |
| Tampered package/model | Signature + hash + manifest verification |
| MAC spoof | Device key + fingerprint |
| Clock rollback | Last-known trusted time |
| Grant rollback | Monotonic revision/sequence |
| Request replay | Nonce, request hash, expiry, idempotency |
| Tenant escape | Tenant-scoped auth/query tests |
| Update failure | Staging, health check, rollback |

VAPT covers enrollment, authz, tenant isolation, signing gateway, offline import/export, artifact upload, update execution, replay/rollback and rehost/transfer.