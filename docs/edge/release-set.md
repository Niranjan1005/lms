# Release Set & Rollback Contract

A deployment is committed as a coherent Release Set, not a collection of independently active files. This prevents application/plugin/model/config combinations that have never been validated together.

## Release Set content

~~~yaml
release_set_id: rs_2026_10_18_01
application: 5.8.0
features:
  ppe: 4.2.1
ui: 2.5.0
runtime: 3.7.0
models:
  ppe_detector: 7.3.0
config_schema: 6
manifest_version: 1
~~~

## Invariants

- one Release Set is Active at a time for a product runtime scope
- Active points only to a health-validated committed set
- the immediately previous known-good set is retained
- every referenced artifact/model is hash/signature verified
- model/runtime/plugin compatibility is resolved before commit
- rollback restores compatible config/schema/model state together

## Update transaction

1. resolve target Release Set and source-version compatibility
2. preflight license/update rights, dependencies, disk, local capacity and maintenance policy
3. reserve/preserve previous known-good set
4. fetch/import only missing verified artifacts
5. verify manifest and every artifact
6. stage in non-active location
7. run signed migration/install handlers
8. start target services and model warm-up
9. execute health/readiness probes
10. atomically switch Active pointer/state
11. emit installation receipt

## Rollback transaction

Rollback is triggered by failed migration/start/health, automatic rollout policy or authorized operator action. It:
1. stops/isolates failed target services
2. restores previous application/plugin/UI/runtime versions
3. restores compatible model set
4. restores compatible configuration/schema snapshot/path
5. starts previous services
6. validates rollback health
7. records rollback result/receipt

## Retention

Immediately previous known-good Release Set is mandatory. Retain 2–3 known-good sets where disk permits. Cleanup SHALL never delete the only locally known rollback path before a new release is proven healthy.

## Interrupted install/restart

Update state is durable. After process/device restart, Update Manager determines whether it can safely resume staging or must rollback; it must not mark a partially installed set Active merely because files exist.

## Model-only update

A model-only deployment still creates/updates the coherent Release Set identity so support and rollback can reconstruct the exact active combination.

## Related SDR

`SDR-OTA-008`, `SDR-OTA-009`, `SDR-MOD-006`, `SDR-MOD-007`