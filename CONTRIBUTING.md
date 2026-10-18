# Contributing to LMS

This repository uses docs-as-code governance for the LMS engineering handbook.

## Workflow

1. Create a short-lived branch from `main`.
2. Make code/documentation changes together when behavior changes.
3. Run `mkdocs build --strict` locally for handbook changes.
4. Open a pull request using the repository template.
5. Obtain required domain/security reviewers.
6. Merge only after CI and review gates pass.

## Documentation standard

Use normative language deliberately:
- **must** / **must not** for required controls
- **should** for recommended baseline
- **may** for allowed optional behavior

Mark unresolved items as **Open Decision** rather than inventing implementation detail.

## Architecture decisions

Create an ADR for material changes to trust boundaries, cryptography, deployment topology, persistence model, public API compatibility, licensing semantics or update architecture.

## Diagrams

Prefer Mermaid for maintainable architecture/sequence/state/ER diagrams. Keep diagrams synchronized with text.

## Sensitive information

Never commit credentials, private keys, production customer exports, raw secrets, decrypted model binaries or incident evidence containing sensitive customer data.