# Security Control Baseline

This is the minimum production security baseline. Customer or regulatory requirements may add controls, but deployment configuration must not silently weaken the non-relaxable requirements below.

## Human identity and privileged access

- deny-by-default authorization
- unique human accounts; no shared administrator credentials
- production target: OIDC/SSO integration
- MFA required for privileged/vendor administration where the chosen IdP supports it
- short-lived sessions/tokens with revocation
- privileged role assignment/removal is audited
- dormant/terminated account access is revoked promptly
- emergency/break-glass access is separately controlled, time-bounded and reviewed
- periodic access review for global/vendor privileged roles

## Device authentication

- device generates/holds its own asymmetric key pair
- enrollment authorization is high-entropy, short-lived and single-use
- central registry stores public key/key ID and fingerprint evidence
- MAC address is never sufficient identity
- requests that change sensitive device state are authenticated by registered device identity or an explicitly defined secure bootstrap flow
- major device-key/identity changes require rehost/re-enrollment approval

## Authorization

- permission + scope evaluation at service/use-case boundary
- customer/site/device ownership validated server-side
- support/global permissions are explicit; no implicit tenant bypass
- maker-checker for sensitive actions
- authorization is never UI-only
- background jobs and asynchronous messages carry tenant scope

## Network and transport

- TLS for external production HTTP/API traffic
- approved modern TLS versions/cipher policy set by deployment baseline
- certificate validation is mandatory; insecure verification bypasses are prohibited
- internal service endpoints are bound to least-exposed interfaces
- local-only edge APIs are not externally reachable by default
- production admin interfaces should be restricted by network policy where deployable

## Application security

- strict request/file input validation
- bounded archive/package extraction
- path traversal, symlink escape and archive-bomb protection
- MIME/file-type and manifest allowlisting for uploaded artifacts
- CSRF controls when cookie authentication is used
- CORS restricted to approved origins
- secure portal headers
- rate limiting for authentication, enrollment and import abuse surfaces
- safe deserialization; no execution of unsigned inline commands
- SSRF-sensitive integrations use destination allowlists where applicable

## Secrets management

- secrets are never committed to source control
- production secrets come from an approved secret manager/KMS/deployment secret store
- secrets are scoped per environment and service
- credentials support rotation without code changes
- secret values are redacted from logs/errors
- database/service credentials use least privilege
- development/test credentials are never valid in production

## Data protection

- encrypted backups
- database and artifact storage encryption at rest where supported by platform/deployment
- model artifacts encrypted in storage/distribution
- highly restricted key material is stored only in protected key systems
- sensitive exports are authorization-scoped and auditable
- no passwords, raw auth tokens, private keys, model content keys or decrypted models in normal logs

## Signing and cryptography

- separate license-signing and release-signing key purposes
- production key custody through KMS/HSM/equivalent protected service
- key ID and algorithm recorded in signed objects
- deterministic canonicalization
- signature verification fails closed
- trust-store/key rotation is versioned and tested
- compromise recovery is documented before production
- use approved crypto libraries; no custom cryptographic primitives

## Offline package security

- device-signed canonical request
- request ID + nonce + expiry + device binding
- central replay/idempotency checks
- response bound to originating request/device
- signatures verified before processing executable/decryptable content
- package import performed in staging/quarantine area
- bounded file count/size/path
- unknown executable content rejected
- signed receipt generated after accepted activation/install

## Edge local security

- device private key stored using strongest practical platform protection
- monotonic accepted grant revision persisted
- last-known trusted time persisted
- product runtime checks authorization at execution boundaries
- update installation runs with least privilege practical for platform
- rollback state protected from untrusted package content
- local APIs bind to loopback/local IPC unless explicitly required otherwise

## Secure SDLC

Threat review -> code review -> unit/integration/security tests -> SAST/SCA/secret scan -> package/provenance checks -> QA -> VAPT where required -> remediation/disposition -> release approval.

## Non-relaxable controls

The following cannot be disabled by customer/site/device policy: signature verification, tenant authorization, private-key separation, anti-replay binding for offline packages, production secret isolation, audit of privileged actions and rejection of invalid/tampered signed content.