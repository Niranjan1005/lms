# Combined Workload Planning

Capacity planning evaluates the complete active and proposed workload, not individual feature quotas in isolation.

~~~mermaid
flowchart TD
    A[Collect Inventory] --> B[Compatibility Check]
    B --> C[Load Existing Workloads]
    C --> D[Add Proposed Workload]
    D --> E[Resolve Approved Benchmark Profiles]
    E --> F[Calculate Combined CPU/RAM/GPU/VRAM/Decode/Disk/Thermal Budget]
    F --> G[Apply Performance + Headroom Targets]
    G --> H{PASS / WARNING / FAIL}
    H -->|PASS| I[Recommend Activation]
    H -->|WARNING| J[Recommend Approved Alternatives]
    H -->|FAIL| K[Block Normal Activation + Recommend Alternatives]
    I --> L[Local Authoritative Recheck]
    J --> L
    K --> L
~~~

## Example

Commercial entitlement:

~~~text
People Counting = 8 cameras
PPE = 4 cameras
~~~

The Capacity Engine does **not** assume 8 + 4 = 12 cameras is feasible. It evaluates the real combined workload using model/runtime/resolution/FPS/decode and concurrency evidence.

If the selected workload does not meet target performance, recommendations may include:

- People Counting 8 + PPE 2
- People Counting 4 + PPE 4
- lower FPS
- lower resolution
- different decode path
- optimized model/runtime
- move a workload to another device
- deploy a second device
- hardware upgrade

The operator/customer chooses an allowed configuration. Purchased entitlement remains unchanged.

## Output

A capacity assessment should return:

- result: pass / warning / fail / stale
- limiting resource(s)
- compatibility blockers
- benchmark profile/version
- workload hash/input summary
- expected/observed headroom
- confidence/evidence quality
- recommendations
- assessment timestamp and freshness
- whether local revalidation is required