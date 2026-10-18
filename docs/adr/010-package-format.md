# ADR-010 — Release Package Format

**Status:** Proposed  
**Decision class:** Edge / Release Format

## Context

ADR-004 selected traditional signed packages instead of a Docker dependency, but the exact archive/container, script-handler contract and platform abstraction must be frozen before Update Manager implementation stabilizes.

## Proposed baseline

A release package contains a signed canonical manifest plus immutable referenced artifacts for application, UI/runtime, dependencies, migrations, configuration templates, install handler, rollback handler and health check. Models may be separate encrypted artifacts referenced by the Release Set.

## Requirements for the final format

- deterministic/canonical manifest serialization
- explicit format/schema version
- bounded archive size/file count/path rules
- content hashes for every artifact
- signed handler artifacts; no unsigned inline commands
- Linux handler implementation first
- Windows-compatible handler abstraction
- staged extraction and execution
- source-version/config-schema compatibility declaration
- health and rollback contract
- offline media friendly
- delta/missing-artifact reuse support

## Options to decide

1. ZIP-based package
2. tar-based package with constrained compression
3. directory/manifests downloaded as separate immutable objects and assembled locally
4. hybrid bundle with manifest plus externally referenced artifacts

## Decision criteria

Security of extraction, cross-platform implementation, large model handling, offline transport, streaming/delta support, tooling availability and reproducibility.

## Rejected direction

Arbitrary installer scripts copied manually to customer sites are not acceptable.

## Decision deadline

Before Update Manager package parser/executor implementation freeze.

## Related requirements

`SDR-PLT-004`, `SDR-OTA-006` through `SDR-OTA-010`