# ADR-008 — Production Human Authentication

**Status:** Open Decision  
**Decision class:** Security / Identity Architecture

## Context

Local development can begin with username/password authentication, but enterprise production deployments commonly require federation, MFA, account lifecycle and customer identity-provider integration. Authorization/RBAC must not be coupled to one identity provider.

## Constraints already approved

- authorization evaluates permission + scope independently from authentication provider
- unique human identities; no shared administrators
- privileged authentication events are audited
- privileged/vendor access targets MFA where supported
- break-glass access is separately controlled and reviewed
- device identity remains separate from human identity

## Options to decide

1. OIDC-only production profile
2. OIDC + SAML adapter boundary if customer demand requires it
3. vendor-managed local accounts for selected customer-hosted deployments as an exception
4. MFA enforcement at IdP versus LMS step-up for selected privileged actions

## Decision criteria

- SaaS and customer-hosted support
- enterprise IdP compatibility
- MFA assurance
- account deprovisioning/revocation
- offline customer-hosted administration requirements
- operational complexity
- supportability

## Consequence until resolved

Implementation SHALL keep authentication behind an adapter and SHALL NOT embed authorization/business rules into username/password-specific code.

## Decision deadline

Must be resolved before production security freeze and external customer onboarding.

## Related requirements

`SDR-SEC-001`, `SDR-SEC-002`