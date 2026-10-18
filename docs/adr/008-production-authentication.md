# ADR-008 — Production Human Authentication

**Status:** Open Decision

## Context

Development begins with username/password. Production enterprise deployments may require OIDC/SSO, MFA and customer identity-provider integration.

## Decision required

Select the production authentication profile and deployment-specific identity-provider integration model before production readiness freeze. Authorization/RBAC is designed independently so the decision does not rewrite domain permissions.