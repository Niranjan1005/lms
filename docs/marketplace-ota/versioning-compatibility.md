# Versioning & Compatibility Policy

## Semantic versioning intent

Application, feature/plugin and model versions should use a predictable version scheme. Semantic versioning is recommended for software interfaces where practical.

## Compatibility declarations

Every release declares supported:
- OS/version and architecture
- application/runtime ranges
- dependent feature/plugin ranges
- model ranges
- configuration schema versions
- minimum hardware/runtime requirements

## Support window

The organization must define how many previous application versions remain upgrade-supported. Until finalized, release manifests must explicitly declare supported source versions rather than assuming any historical version can upgrade directly.

## Breaking changes

Breaking local API, manifest or grant-format changes require:
1. schema/version bump
2. compatibility/migration plan
3. dual-read or staged migration when necessary
4. explicit support-window communication
5. rollback testing

## Model compatibility

Model releases are independently versioned but must declare compatible feature/runtime ranges. A model-only update is allowed only when those constraints pass.