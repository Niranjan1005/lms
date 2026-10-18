# Architecture Decision Records

ADRs preserve the reason behind durable architecture decisions and separate approved baselines from unresolved security/product choices.

| ADR | Title | Status |
|---|---|---|
| ADR-001 | Digitally Signed Grants | Approved |
| ADR-002 | Modular Monolith First | Approved |
| ADR-003 | Marketplace & OTA Inside LMS | Approved |
| ADR-004 | Traditional Signed Release Packages | Approved |
| ADR-005 | Device-Generated Cryptographic Identity | Approved |
| ADR-006 | Separate License and Release Signing Keys | Approved |
| ADR-007 | Signed Offline Request/Response | Approved |
| ADR-008 | Production Human Authentication | Open Decision |
| ADR-009 | Model Encryption and Key Wrapping | Open Security Decision |
| ADR-010 | Release Package Format | Proposed |

## ADR template

~~~text
# ADR-XXX — Title

Status: Proposed | Approved | Open Decision | Deprecated
Date: YYYY-MM-DD

## Context
## Decision
## Alternatives Considered
## Consequences
## Security / Operational Impact
## Follow-up
~~~

Approved ADRs may only be superseded by a newer ADR; do not silently rewrite historical decisions.