# Security Control Baseline

This is the minimum security baseline for development and release readiness. It does not replace customer-specific compliance requirements.

## Identity and access

- deny-by-default RBAC
- password hashing using an approved adaptive password hash in development auth
- privileged role changes audited
- no shared administrator accounts
- session/token expiry and revocation
- future production IAM adapter without rewriting authorization model

## Application security

- input validation at all API/file-import boundaries
- allowlisted parsers and bounded archive extraction
- protection against path traversal and archive bombs
- CSRF protection where cookie sessions are used
- CORS restricted by deployment policy
- rate limiting for login/enrollment/import abuse surfaces
- secure headers for portal
- dependency/SCA and SAST in CI

## Data security

- TLS for central network transport
- secrets outside source control
- database least-privilege credentials
- encrypted backups
- artifact integrity by hash and signature
- model artifacts encrypted in storage/distribution
- no raw passwords/private keys/decrypted models in logs

## Signing boundary

- separate license-signing and release-signing key purpose
- key ID/version recorded in artifacts
- rotation supported without breaking old verification immediately
- signing request authorization and audit
- production custody via KMS/HSM/equivalent protected service where feasible

## Offline import security

- signed/canonical request payload
- nonce/request ID and expiry
- device binding
- anti-replay storage
- strict package size/content validation
- signatures checked before execution/decryption

## Secure SDLC gates

Threat review -> code review -> automated security scan -> QA -> VAPT as required -> remediation -> release approval.