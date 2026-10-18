# Combined Workload Planning

~~~mermaid
flowchart TD
    A[Collect Inventory] --> B[Existing Workloads]
    B --> C[Proposed Feature]
    C --> D[Benchmark Profiles]
    D --> E[Combined Resource Budget]
    E --> F{Meets Target?}
    F -->|Yes| G[Recommend Activation]
    F -->|Warning| H[Recommend Alternatives]
    F -->|No| I[Different Allocation / Hardware]
~~~

Alternatives may include fewer active cameras with approval, lower FPS/resolution, optimized model/runtime, moving workload, or hardware upgrade.