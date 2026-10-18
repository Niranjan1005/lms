# Human Identity, Session & Privileged Access Security

Development username/password auth is a bootstrap implementation. Production human identity remains an open ADR, but the authorization and session control baseline is defined now.

## Production target

- OIDC/SSO adapter for enterprise identity providers
- MFA for privileged/vendor administration where supported
- role mapping that does not grant global privilege by default
- explicit logout/revocation and session expiry
- audit of login success/failure and privileged authentication events

## Bootstrap/local password mode

Where username/password mode is permitted:
- adaptive password hashing (Argon2id or approved equivalent)
- minimum password policy enforced by deployment/security profile
- rate limiting and progressive abuse protection
- no plaintext/reversible password storage
- password reset tokens are short-lived, single-use and securely random
- reset does not reveal whether arbitrary accounts exist

## Session/token baseline

- short-lived access token/session
- refresh/session rotation when applicable
- server-side revocation capability for privileged sessions
- audience/issuer validation for external IdP tokens
- clock-skew tolerance is bounded
- tokens never accepted from query strings
- token/session identifiers redacted from logs

## Privileged access

- global/vendor privileged roles granted explicitly
- periodic access review
- privilege elevation/role changes generate audit events
- sensitive actions may require fresh authentication or second approval
- support access remains customer-scoped unless explicitly elevated

## Break-glass

Emergency access is separate from normal administration, tightly limited, auditable, time-bounded and reviewed after use. Break-glass credentials/tokens are not shared in normal documentation or chat systems.

## Device versus human identity

Human sessions and device cryptographic identity are separate security principals. Human login credentials are never used as the device's long-lived identity.