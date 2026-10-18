# Release Set & Rollback Contract

A deployment is defined as a coherent release set rather than an isolated application file.

## Example release set

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
~~~

## Update transaction

1. Preflight compatibility, disk and policy checks.
2. Preserve current known-good release set.
3. Fetch/import only missing artifacts.
4. Verify every artifact.
5. Run automated config/database migrations.
6. Start target services.
7. Run warm-up and health probes.
8. Atomically mark release set active.
9. On failure restore previous release set and compatible config/model state.

Retention: compress and retain 2–3 known-good sets where storage permits; immediately previous known-good set is mandatory.