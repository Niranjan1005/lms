# Reassessment & Runtime Monitoring

Capacity is not a one-time registration result. Assessments become stale when relevant conditions change.

## Mandatory reassessment triggers

- hardware inventory change
- GPU/accelerator or driver change
- CUDA/TensorRT/DeepStream/runtime change
- application/feature release change
- model version change
- camera count/resolution/FPS/codec change
- new feature activation
- feature deactivation that changes combined workload
- site-to-device workload movement
- benchmark profile superseded by a materially different approved profile
- repeated runtime degradation or thermal throttling

## Runtime monitoring signals

Where available, monitor:
- achieved inference/processed FPS
- p95/p99 inference latency
- dropped/late frames
- CPU/GPU utilization
- VRAM/RAM pressure
- decoder utilization
- temperature/throttling
- service health/restarts
- active stream count

## Drift handling

~~~text
Healthy -> Warning -> Reassess -> Recommendation / Operator Action
                     |
                     +-> Critical degradation -> protect service / fail feature according to runtime safety policy
~~~

Runtime degradation does not rewrite entitlement. It may trigger a new capacity assessment and recommendation.

## Assessment freshness

Each assessment records inventory version, resource snapshot timestamp, workload hash, benchmark version and software/model versions. If any required input changes, the previous assessment becomes stale.

## Central vs local drift

Central LMS may show an advisory result based on last reported evidence. The local Capacity Engine remains authoritative for activation because it can detect current real conditions.

## Telemetry integration

Capacity history may be forwarded to telemetry/analytics for trend analysis, but transactional activation state stays in the operational LMS/device state model.