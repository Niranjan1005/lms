# Deployment & Rollback

Deployment turns an approved release set into per-device installation actions with policy, maintenance-window, concurrency, health and rollback controls.

## Policy hierarchy

~~~text
Platform Default -> Product -> Customer -> Site -> Device Override
~~~

Supported settings include AUTO/MANUAL, channel, maintenance window, model-only OTA, application OTA, concurrency, rollout batch size and auto-rollback.

Default automatic maintenance window: 01:00–03:00 in site timezone, customer configurable.

## Target resolution

Before scheduling, LMS resolves target customer/site/device ownership, entitlement/update rights, device status, compatible release-set path and maintenance policy. A target that becomes ineligible before install is revalidated and blocked.

## Rollout strategies

- all-at-once only for explicitly accepted small/low-risk scope
- batch/concurrency-limited rollout
- canary/pilot subset before broader rollout where risk warrants
- pause/stop on configured failure threshold
- forced rollout requires privileged approval when policy marks it sensitive

## Per-target execution

~~~text
Pending -> Waiting Window -> Preflight -> Download/Import -> Verify -> Stage -> Install -> Health Check -> Active
                                                              |
                                                              +-> Rollback -> Rolled Back
~~~

## Preflight gates

- release/channel eligibility
- current/source version supported
- grant/update right valid
- OS/architecture/runtime compatible
- dependencies/model versions resolvable
- disk space and rollback reserve
- local capacity check
- package/trust-store compatibility

## Success semantics

A target is successful only after health check and atomic commit. Downloaded or installed files alone do not mean Active.

## Rollback

Rollback restores a coherent release set, not one binary. Keep 2–3 known-good releases when disk permits; the immediately previous known-good set is mandatory.

## Automatic stop criteria

Systemic signature/hash failure, repeated migration failure, rollback failure, or failure-rate threshold should stop/pause further rollout and alert Release/Operations.

## Offline deployment

Air-gapped deployment uses the same target/release semantics. The response bundle carries required release-set artifacts; final central state becomes authoritative only after signed installation receipt reconciliation.