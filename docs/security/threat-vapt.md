# Threat Model & VAPT

| Threat | Baseline control |
|---|---|
| Enrollment/token guessing | High entropy, short-lived/single-use authorization, rate limiting |
| Forged license | Protected central signing key + digitally signed grants |
| Tampered package/model | Signature + hash + manifest verification |
| MAC spoofing | Device cryptographic key + weighted/versioned fingerprint; MAC only evidence |
| Device cloning | Device-bound grants, protected local key/state, quantity controls |
| Clock rollback | Persist last-known trusted time; suspicious backward jumps cause reject/restrict until revalidation |
| Grant rollback | Monotonic revision/sequence and protected local accepted-state |
| Request replay | Nonce, request hash, expiry, idempotency, device binding |
| Stolen/compromised relay | Transport-only role, short-lived auth, encrypted staging where feasible, no signing authority |
| Tenant escape | Strict tenant-scoped authorization and negative isolation tests |
| Update crash | Atomic staging, health check, coherent release-set rollback |
| Transfer/rehost abuse | Approval, maker-checker for sensitive cases, immutable audit lineage |
| Signing-key compromise | Key-purpose separation, rotation/recovery plan, incident procedure |
| Offline revocation delay | Accepted design limitation; revoke on signed import or offline expiry |
| Fully compromised/root edge | Software signatures/hardening reduce risk but cannot guarantee tamper-proof execution on a hostile root-controlled host |

## VAPT coverage

VAPT/release security validation covers at minimum:

- enrollment
- authentication and authorization
- tenant isolation
- license/grant issuance
- signing gateway
- offline package import/export
- malformed/archive/path traversal inputs
- artifact/model upload and verification
- update execution and rollback
- replay/rollback
- transfer/rehost/decommission
- portal/API privileged actions

High-risk findings must be remediated or explicitly dispositioned before production promotion according to security policy.