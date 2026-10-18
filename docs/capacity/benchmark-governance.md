# Benchmark Profile Governance

Benchmark data is production engineering evidence. It requires versioning, ownership and release discipline.

## Benchmark profile dimensions

A profile may be keyed by:
- hardware class/model
- accelerator/GPU architecture and VRAM
- driver/runtime stack
- feature/model/version
- resolution/FPS/codec
- decode path
- inference backend and precision
- concurrent workloads
- measured latency/FPS/utilization/headroom

## Lifecycle

~~~text
DRAFT -> VALIDATING -> APPROVED -> ACTIVE -> SUPERSEDED -> RETIRED
~~~

Only APPROVED/ACTIVE benchmark profiles may drive production recommendations.

## Evidence requirements

Each benchmark profile records:
- benchmark version
- test hardware identity/class
- software/runtime versions
- test dataset/workload definition
- warm-up period
- sample duration
- measured throughput/latency
- CPU/RAM/GPU/VRAM/decode utilization
- temperature/throttling observations
- target/headroom thresholds
- test date and owner
- approval status

## Matching

The Capacity Engine chooses the closest valid profile using explicit compatibility rules. It must not silently use a materially different hardware/runtime profile without reducing confidence or marking the result unsupported.

## Confidence

Suggested confidence categories:
- high: exact or validated-equivalent profile
- medium: approved near-match with bounded interpolation
- low: weak match; recommendation only, activation may require local empirical validation
- unsupported: no valid evidence

## Headroom

Capacity results should expose remaining headroom for limiting resources when measurable. Example: GPU compute headroom 14%, VRAM headroom 22%, CPU headroom 35%.

Thresholds are product/benchmark policy, not hard-coded globally.