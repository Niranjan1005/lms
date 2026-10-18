# Core Sequence Diagrams

This page defines implementation-level interaction expectations between the central LMS and edge/application components.

## First-time registration and base activation

~~~mermaid
sequenceDiagram
    actor A as Vendor Admin
    participant P as LMS Portal/API
    participant D as Device Agent
    participant R as Device Registry
    participant C as Capacity Service
    participant E as Entitlement Engine
    participant S as Signing Service
    participant L as Local License Agent
    A->>P: Create customer/site + enrollment authorization
    D->>P: Enrollment request + public key + fingerprint + inventory
    P->>R: Validate token, ownership, duplicates
    R-->>P: Registered device identity
    P->>C: Pre-assess base workload
    C-->>P: Pass / warning / fail + recommendations
    P->>E: Check approved commercial entitlement
    E-->>P: Entitlement + limits
    P->>S: Sign device-bound base grant
    S-->>P: Signed grant
    P-->>D: Deliver grant
    D->>L: Import grant
    L->>L: Verify signature, binding, term, revision
    L->>L: Local capacity + health validation
    L-->>P: Activation receipt when connected
~~~

## Add-on trial or purchase

~~~mermaid
sequenceDiagram
    actor U as Customer/Admin
    participant M as Marketplace
    participant C as Capacity Service
    participant E as Entitlement/Policy
    participant R as Release Service
    participant D as Device
    U->>M: Select feature
    M->>C: Compatibility + combined workload pre-check
    C-->>M: Feasibility result
    U->>M: Start trial or request purchase
    M->>E: Validate eligibility/commercial approval
    E-->>M: Approved grant parameters
    M->>R: Resolve compatible release set
    R-->>M: App/UI/model/dependency set
    M-->>D: Signed grant + required artifacts
    D->>D: Verify, re-check capacity, stage, health-check
    D-->>M: Activation / installation receipt
~~~

## Renewal for offline device

~~~mermaid
sequenceDiagram
    actor U as Customer
    participant L as LMS
    participant S as Signing Service
    participant O as Offline Relay
    participant D as Device
    U->>L: Renewal request / commercial approval
    L->>S: Sign superseding grant revision
    S-->>L: Signed renewed grant
    L-->>O: Export response package
    O-->>D: Controlled-media transfer
    D->>D: Verify revision, binding, term, supersession
    D-->>O: Signed acceptance receipt
    O-->>L: Reconcile receipt
~~~