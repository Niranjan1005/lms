# Licensing Overview

~~~mermaid
flowchart LR
    E[Customer Entitlement Pool] --> A[Allocation]
    A --> G[Device-bound Signed Grant]
    G --> V[Local Verification]
    V --> R[Runtime Permission]
~~~

This separates commercial ownership from device execution.