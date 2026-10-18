# Software Supply-Chain Security

## Required controls

- source changes through reviewed pull requests
- protected production release branch/tag process
- pinned/controlled dependencies
- SCA/dependency vulnerability scanning
- SAST and secret scanning
- build provenance/traceability to source commit
- SBOM generation for production release packages
- signed immutable release manifests/artifacts
- malware/file-type scanning for uploaded artifacts where applicable
- separation of development signing and production release signing

## Artifact provenance

A production artifact must be traceable to source commit/tag, CI build identity, build environment/version, dependency/SBOM record, test/security evidence, release manifest and signing key ID.

## Third-party dependencies

Critical CVEs are triaged against exploitability and exposure. Approved remediation windows and exception process must be defined by Security/Engineering governance.

## Build environment

Production builds should be reproducible or at minimum controlled and isolated. Build agents must not persist production signing secrets; signing occurs through protected provider integration.

## Release gate

A release with unresolved prohibited-severity supply-chain findings cannot be promoted to Stable/LTS without explicit security disposition.