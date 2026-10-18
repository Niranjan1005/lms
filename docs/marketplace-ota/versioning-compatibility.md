# Versioning & Compatibility Policy

Versioning is a contract between central LMS, edge components, release packages and models. A version string alone is insufficient; every release declares what it can safely run with and upgrade from.

## Version domains

- LMS central application/API
- edge application
- feature/plugin
- local component/interface
- manifest/package schema
- configuration schema
- model
- grant schema/canonicalization
- offline request/response schema

Semantic Versioning is preferred for software interfaces where practical, but compatibility declarations are authoritative.

## Release compatibility declaration

Every deployable release declares:
- product
- OS/version + architecture
- supported source application versions
- runtime/framework ranges
- feature/plugin dependency ranges
- model ID/version ranges
- config schema range/target
- required manifest/local interface versions
- minimum hardware/runtime prerequisites
- migration path
- rollback compatibility

## Compatibility result

~~~text
COMPATIBLE
INCOMPATIBLE
UPGRADE_PATH_REQUIRED
UNKNOWN / UNSUPPORTED
~~~

Unknown is not treated as compatible for automatic production deployment.

## Upgrade paths

Release manifests explicitly declare supported source versions. If a customer is too old for a direct jump, LMS/Update Manager identifies the required intermediate release rather than attempting an unsupported migration.

## Breaking changes

Breaking local API, manifest, offline protocol or grant schema changes require:
1. version/schema bump
2. compatibility/migration plan
3. staged/dual-read strategy where needed
4. support-window communication
5. old/new contract tests
6. rollback/forward-recovery validation

## Model compatibility

Models are independently versioned and declare compatible feature/runtime/hardware ranges. Model-only OTA is permitted only when these constraints and local capacity/health checks pass.

## Central-edge compatibility

Central LMS must remain able to serve supported historical edge versions during their declared support window. APIs/offline package builders should not assume all devices upgrade simultaneously.

## Retirement/support window

The organization must finalize how many historical application versions remain supported. Until then, every release explicitly declares source/support compatibility; no code path assumes indefinite backward compatibility.

## Related SDR

`SDR-OTA-006` through `SDR-OTA-010`, `SDR-MOD-006`, `SDR-BE-006`