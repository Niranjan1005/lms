# Capacity Status Model

Capacity-related states must remain separate from commercial licensing and installation state. UI, API and audit records must not collapse them into one boolean.

## Independent status dimensions

| Dimension | Meaning | Example states |
|---|---|---|
| Licensed | Customer/device has valid commercial authorization | not_entitled, entitled, grant_pending, grant_active |
| Compatible | Software/model can technically run on this platform/runtime | unknown, compatible, incompatible, blocked_dependency |
| Capacity validated | Combined workload is expected to meet the defined performance target | not_assessed, pass, warning, fail, stale |
| Installed / healthy | Required application/model components are present and healthy | not_installed, staged, healthy, degraded, failed |

These dimensions are evaluated independently and then combined for activation.

## Activation rule

~~~text
Licensed
AND Compatible
AND Capacity Validated
AND Installed / Healthy
= Feature may activate
~~~

A commercial entitlement can be valid even when the device is incompatible or under-capacity. Capacity failure never removes purchased entitlement.

## Capacity result semantics

**PASS** — benchmark evidence and current local conditions meet target with required headroom.

**WARNING** — workload is likely feasible but headroom/confidence is below preferred target, or the operator must choose an allowed lower-load configuration.

**FAIL** — the selected combined workload does not meet the minimum activation target.

**STALE** — the assessment is no longer valid because inventory, runtime, model, workload or benchmark policy changed.

## Reason-code examples

~~~text
CAP_GPU_VRAM_INSUFFICIENT
CAP_GPU_COMPUTE_BELOW_TARGET
CAP_CPU_HEADROOM_LOW
CAP_RAM_HEADROOM_LOW
CAP_DISK_FREE_LOW
CAP_RUNTIME_UNSUPPORTED
CAP_DRIVER_MISMATCH
CAP_DECODE_BUDGET_EXCEEDED
CAP_COMBINED_WORKLOAD_EXCEEDS_PROFILE
CAP_BENCHMARK_PROFILE_MISSING
CAP_INVENTORY_STALE
CAP_RESOURCE_SNAPSHOT_STALE
~~~

Reason codes are stable machine-readable values and map to operator-safe recommendations.