# Inventory & Benchmarking

Stable inventory and dynamic resource snapshots are stored separately.

## Stable inventory

Collect at minimum:

- CPU model, architecture, physical/logical cores and relevant frequency/capability data
- RAM total and configured limits
- GPU model/architecture, VRAM and relevant compute capability
- accelerators such as Jetson/NPU where applicable
- storage total/free/filesystem/health evidence
- OS distribution/version, kernel
- GPU/accelerator drivers
- CUDA, TensorRT, DeepStream and product runtime versions
- camera workload descriptors: count, resolution, FPS, codec/decode requirements
- installed services, application releases and model inventory

## Dynamic snapshots

Capture separately:

- available RAM
- free disk
- GPU/accelerator utilization
- temperature/throttling
- active streams
- active workloads
- other runtime pressure signals needed by the local Capacity Engine

## Benchmark profiles

Capacity decisions use measured, versioned benchmark profiles across:

- hardware class
- analytics model/version
- resolution
- FPS
- inference backend
- decoder/pipeline
- concurrent workloads
- target latency/FPS/SLA

Instantaneous utilization alone is not a benchmark.

Every assessment must record the benchmark profile/version and inventory/workload inputs used so the result can be reproduced and audited.