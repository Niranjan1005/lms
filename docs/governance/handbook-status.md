# Handbook Status, Authority & Ownership

This handbook is the normative internal engineering baseline for LMS unless superseded by a newer approved ADR, formal product/security decision or generated implementation contract explicitly identified as authoritative.

## Status taxonomy

- **Approved** — normative implementation baseline
- **Proposed** — recommended design awaiting approval
- **Open Decision** — constraints are known; implementation must preserve flexibility
- **Superseded** — historical decision replaced by another identified record
- **Deprecated** — retained for history but must not be used for new implementation
- **Phase 2 / Deferred** — intentionally not part of current delivery scope

## Authority order

When documents conflict, use this order unless a record explicitly states otherwise:
1. approved ADR for durable architecture choice
2. approved SDR/business rule for required behavior
3. generated/frozen API/schema contract for implementation details
4. detailed domain handbook section
5. examples/illustrations

A conflict must be corrected; teams should not silently choose whichever page is convenient.

## Change ownership

| Section | Primary approver | Required co-review when applicable |
|---|---|---|
| Product/business rules | Product/leadership | Architecture/QA |
| SDR / Architecture | Architecture/Tech Lead | Product/Security/Edge |
| ADRs | Architecture owner | domain owner + Security for trust changes |
| Licensing/grants | Backend + Product | Security/Edge |
| Capacity | Performance/AI + Architecture | Edge/Product |
| Marketplace/OTA | Product + Release | Edge/Security/QA |
| Edge enforcement/update | Edge Lead | Security/Backend/QA |
| Security/crypto | Security | Architecture/DevOps/Edge |
| Backend/data/API | Backend Lead | Security/QA |
| QA/release gates | QA/Release Manager | domain owner/Security |
| Operations/DR | DevOps/Operations | Security/Backend |

## Required maintenance

A change that modifies observable behavior, business rule, API/event schema, persistent model, trust boundary, release/package format, local edge contract, operational recovery or security control updates the affected handbook/SDR/ADR in the same PR.

## Review cadence

- release-affecting sections reviewed during release readiness
- security/DR/runbooks reviewed after incidents/material architecture changes
- open decisions reviewed at the milestone/deadline recorded in their owning document
- stale examples/defaults corrected when product policy changes

## Historical integrity

Approved ADRs are historical records; material reversal uses supersession instead of silently rewriting the past decision. Other handbook pages may be edited in place but must preserve change traceability through Git.

## Content quality rule

A page is not considered complete because it exists. Completion requires enough detail to implement, test and operate the behavior or an explicit link to the authoritative detailed specification.