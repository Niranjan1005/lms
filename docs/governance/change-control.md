# Engineering Change Control

Tier-1 governance requires traceability from business decision to code and production release.

## Change classes

| Class | Example | Required controls |
|---|---|---|
| Standard | bug fix, docs, non-risk refactor | PR + tests + review |
| Architecture | new module, trust boundary, schema model | ADR + architecture review + PR |
| Security-sensitive | signing, auth, import parser, model protection | security review + tests + VAPT scope review |
| Commercial-policy | entitlement, expiry, trial, renewal rules | product/commercial approval + regression tests |
| Emergency | critical security/production issue | expedited approval + complete post-change review |

## Traceability

Every material production change should be traceable to requirement/issue, design/ADR where relevant, pull request, CI evidence, release identifier and deployment/audit event.