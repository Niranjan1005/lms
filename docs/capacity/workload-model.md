# Workload Model

Capacity planning is based on actual workload characteristics rather than licensed quantity alone.

## Workload dimensions

A workload profile should capture, where relevant:
- feature/capability code
- analytics model ID and version
- camera/input count
- per-input resolution
- FPS
- codec
- decode path (CPU/GPU/hardware decoder)
- inference backend
- precision
- batching/concurrency
- preprocessing/postprocessing cost class
- retention/output pipeline impact where applicable
- site assignment
- required performance target such as minimum processed FPS or maximum latency

## Example workload

~~~json
{
  "feature_id": "ppe_detection",
  "model_id": "ppe_detector",
  "model_version": "7.3.0",
  "site_id": "site_a",
  "inputs": {
    "camera_count": 4,
    "resolution": "1920x1080",
    "fps": 10,
    "codec": "h264",
    "decode_path": "gpu"
  },
  "runtime": {
    "backend": "tensorrt",
    "precision": "fp16"
  },
  "target": {
    "min_processed_fps": 9.5,
    "max_p95_latency_ms": 250
  }
}
~~~

## Combined workload budget

The Capacity Engine evaluates all active workloads plus the proposed workload together.

~~~text
Existing workload A
+ Existing workload B
+ Proposed workload C
----------------------
Combined CPU / RAM / GPU / VRAM / decode / storage / thermal budget
~~~

Licensed quotas must not simply be added and treated as capacity.

## Multi-site devices

For a device serving multiple sites, the workload model retains site attribution but capacity is evaluated at the shared device resource level. Site limits constrain commercial use; shared hardware capacity constrains actual concurrent execution.

## Workload identity

Persist a stable workload profile or canonical workload hash so assessments can be reproduced and compared over time.