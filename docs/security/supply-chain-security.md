# Software Supply-Chain Security

Supply-chain security covers source, dependencies, build systems, release metadata, artifact provenance and promotion. A valid runtime signature is necessary but not sufficient if the build/source pipeline itself is compromised.

## Source controls
- reviewed pull requests for production code/config
- protected main/release refs according to repository policy
- traceability from issue/SDR/ADR to commit/PR
- no production credentials or private keys in source
- security-sensitive paths require domain review

## Dependency controls
- pinned/constrained dependencies
- software composition analysis (SCA)
- transitive dependency visibility
- vulnerability triage by exploitability/exposure
- approved exception with owner/expiry for unresolved risk
- unused/high-risk dependencies removed where practical

## Build controls
- controlled CI/build environment
- build identity linked to source commit/tag
- isolated production build credentials
- build agents do not persist production signing private keys
- deterministic/reproducible build preferred; otherwise environment/tool versions recorded
- generated artifacts are never manually replaced after publication

## Provenance
A production release is traceable to:
~~~text
source commit/tag
  -> CI workflow/run/build identity
  -> dependency lock/SBOM
  -> test/security evidence
  -> artifact hashes
  -> signed manifest
  -> signing key ID
  -> release promotion record
~~~

## SBOM
Stable/LTS release packages SHALL produce an SBOM covering application/runtime/package dependencies according to supported tooling. SBOM is retained with release evidence and used for vulnerability impact analysis.

## Artifact intake
Uploaded third-party/customer/vendor artifacts are type/size validated, scanned where applicable, hashed and staged before publication. Repository location does not make content trusted.

## Signing separation
Development signing and production release signing are separate. Production signing occurs only after release eligibility/evidence is validated according to release workflow.

## Promotion
Development/QA artifacts are not implicitly production artifacts. Stable promotion records exact immutable artifact identities/hashes and approvals.

## Compromise response
Suspected build/dependency/repository compromise blocks affected releases, preserves provenance evidence, identifies downstream releases/devices, rotates exposed credentials and rebuilds/reissues artifacts as new identities if required.

## Release gate
Unresolved prohibited-severity supply-chain finding blocks Stable/LTS unless Security formally accepts/documented exception according to vulnerability policy.

## Related SDR
`SDR-SEC-009`, `SDR-QA-007`