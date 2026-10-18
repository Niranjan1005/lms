# Inventory & Benchmarking

Capacity decisions must be reproducible. Stable hardware facts, dynamic runtime pressure and benchmark evidence are separate datasets with independent timestamps/versions.

## Stable inventory

Collect at minimum:
- CPU model, architecture, physical/logical cores, ISA/capability flags and relevant frequency data
- RAM total/configured limits
- GPU model/architecture, VRAM, compute capability
- accelerator/NPU/Jetson identifiers where applicable
- storage total/free/filesystem/device health evidence
- OS distribution/version, kernel
- GPU/accelerator driver
- CUDA/TensorRT/DeepStream/product runtime versions
- decoder/media capabilities
- installed application/services/releases
- installed model inventory

## Dynamic resource snapshot

Capture time-specific evidence separately:
- available RAM
- free disk
- CPU utilization/load where relevant
- GPU compute/utilization
- GPU memory used/free
- decoder utilization where available
- temperature/thermal throttling
- active streams
- active workloads and workload hash
- service health/restarts relevant to capacity

Dynamic utilization is evidence of current pressure; it is not itself a benchmark.

## Workload descriptors

Camera/input workloads include count, resolution, FPS, codec, decode path, feature/model version, inference backend/precision, batching/concurrency and performance target. Non-camera products define equivalent workload dimensions.

## Benchmark profile

A benchmark profile records:
- hardware class/exact tested platform
- driver/runtime versions
- feature/model/version
- resolution/FPS/codec/decode path
- backend/precision/batching/concurrency
- test dataset/workload definition
- warm-up and measurement duration
- measured throughput/latency
- CPU/RAM/GPU/VRAM/decode utilization
- temperature/throttling
- pass/headroom targets
- test owner/date
- profile version/status/confidence

## Evidence quality

Assessment matching classifies profile fit, for example:
- high: exact or validated equivalent
- medium: approved bounded near-match
- low: weak approximation requiring local validation
- unsupported: no acceptable profile

The engine must not silently present a low-quality approximation as high-confidence capacity.

## Versioning

Inventory, workload, benchmark profile, app/runtime and model versions used in an assessment are persisted. Material change makes prior result stale according to reassessment rules.

## Benchmark governance

Only approved/active benchmark profiles drive production recommendations. Superseded/retired profiles remain available for historical audit/reproduction.

## Related SDR
`SDR-CAP-002` through `SDR-CAP-005`, `SDR-CAP-011`