# Release Management

Release Management governs creation, evidence, promotion, retirement and supportability of application, feature/plugin, UI/runtime and model-compatible releases.

## Channels

~~~text
Development -> QA -> Internal/Beta -> Stable -> LTS -> Retired
~~~

Channel movement is a controlled promotion, not a file copy.

## Channel semantics

| Channel | Purpose | Production eligible |
|---|---|---|
| Development | developer iteration | No |
| QA | formal test candidate | No |
| Internal/Beta | controlled non-general validation | Restricted |
| Stable | default production release | Yes |
| LTS | explicitly designated long-support release | Yes |
| Retired | blocked from new deployment | No |

Automatic production updates consume Stable by default. LTS targeting is explicitly controlled by the company.

## Release evidence

Before Stable promotion, the release record links to:
- source commit/tag
- CI/build identity
- release manifest and artifact hashes
- automated unit/integration/upgrade tests
- migration result
- rollback result
- compatibility matrix
- capacity/benchmark impact where relevant
- security scan/VAPT disposition
- SBOM/provenance record
- release notes/known issues
- rollout and rollback triggers

## Publication

Published manifests/artifacts are immutable. Correction creates a new release/version. Artifact repository content alone does not make a release deployable; release state and approval govern eligibility.

## Traditional package standard

~~~text
release/
├── manifest.json
├── application/
├── ui/
├── migrations/
├── configs/
├── dependencies/
├── install/
│   ├── install.sh
│   ├── rollback.sh
│   └── healthcheck.sh
└── signature
~~~

Install/migration/rollback handlers are signed artifacts. No normal production release depends on manual site migration.

## Retirement

Retirement prevents new deployment. Existing installations are not silently removed. Support policy determines required upgrade path and emergency-block behavior.

## LTS

LTS designation requires explicit support-life decision, supported upgrade paths, compatibility evidence and operational commitment. Stable does not automatically become LTS.