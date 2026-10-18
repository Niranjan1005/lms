# Handbook Status & Ownership

This handbook is the normative internal engineering baseline for LMS unless a newer approved ADR or product decision supersedes a section.

## Status taxonomy

- **Approved** — implementation baseline.
- **Proposed** — recommended design awaiting approval.
- **Open Decision** — implementation must preserve flexibility until resolved.
- **Deprecated** — retained for historical reference only.
- **Phase 2** — deliberately deferred capability.

## Change ownership

| Section | Primary approver |
|---|---|
| Product/business rules | Product owner / leadership |
| Architecture/ADRs | Architecture/Tech Lead |
| Licensing/grants | Backend + Product |
| Edge enforcement/update | Edge Lead |
| Security/crypto | Security |
| QA/release gates | QA/Release Manager |
| Operations/DR | DevOps/Operations |

## Required maintenance

Any code change that changes observable platform behavior, API contract, schema, release format, security boundary or operational procedure updates the handbook in the same PR.