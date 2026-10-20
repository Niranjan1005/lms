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
    C-->>P: Advisory result
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

## Online trial activation

~~~mermaid
sequenceDiagram
    actor U as Customer Admin
    participant M as Marketplace
    participant P as Policy/Entitlement
    participant C as Capacity
    participant R as Release Service
    participant D as Device
    U->>M: Start trial
    M->>P: Validate eligibility (customer entitlement + feature)
    P-->>M: Eligible + configured duration
    M->>C: Pre-assess workload
    C-->>M: Recommendation/result
    M->>R: Resolve compatible release/model set
    M-->>D: Signed trial grant + required artifacts
    D->>D: Verify + local capacity + install + health-check
    D-->>M: First successful activation receipt
    M->>P: Start trial clock at activation time
~~~

## Offline / air-gapped trial activation

~~~mermaid
sequenceDiagram
    participant D as Device
    participant O as Relay/Media
    participant L as LMS
    participant S as Signing/Artifacts
    D->>O: Export signed trial request + nonce + inventory
    O->>L: Transfer request
    L->>L: Validate trial eligibility + capacity pre-assessment
    L->>S: Create signed trial grant + minimal compatible bundle
    S-->>L: Response package
    L-->>O: Approved response
    O-->>D: Controlled-media import
    D->>D: Verify request binding, grant, artifacts, local capacity
    D->>D: Install + health-check + activate
    D-->>O: Signed activation receipt
    O-->>L: Reconcile receipt
    Note over O,L: Start trial clock after successful activation
~~~

## Feature purchase and add-on activation

~~~mermaid
sequenceDiagram
    actor U as Customer/Admin
    participant M as Marketplace
    participant E as ERP/Commercial
    participant L as LMS Entitlement/Policy
    participant R as Release Service
    participant D as Device
    U->>M: Request purchase
    M->>E: Commercial approval/payment workflow
    E-->>L: Approved commercial state
    L->>L: Create/update entitlement item + allocation
    L->>L: Issue superseding/add-on grant
    L->>R: Resolve compatible package/model set
    R-->>L: Release set
    L-->>D: Grant + release set
    D->>D: Verify dependencies + local capacity + health
    D-->>L: Accepted/active receipt
~~~

## Capacity reassessment after hardware/workload change

~~~mermaid
sequenceDiagram
    participant D as Device
    participant C as Central Capacity
    participant L as Local Capacity
    participant A as Admin
    D->>C: New inventory/resource/workload snapshot
    C->>C: Recalculate using benchmark profile
    C-->>A: Pass/warning/fail + recommendations
    A->>D: Choose approved configuration if adjustment needed
    D->>L: Reassess actual local combined workload
    L-->>D: Authoritative activation decision
    Note over D,L: Commercial entitlement is unchanged
~~~

## Online software/model update

~~~mermaid
sequenceDiagram
    participant L as LMS Deployment
    participant D as Update Manager
    participant R as Runtime
    L-->>D: Deployment target + signed release-set manifest
    D->>D: Preflight license/compatibility/disk/capacity
    D->>L: Fetch only missing artifacts/models
    D->>D: Verify signatures/hashes
    D->>D: Preserve known-good release set
    D->>D: Stage + migrate
    D->>R: Restart/start target services
    R-->>D: Health result
    alt Health OK
      D->>D: Commit target release set
      D-->>L: Installation receipt
    else Health failed
      D->>D: Roll back coherent previous release set
      D-->>L: Failure/rollback receipt
    end
~~~

## Offline software/model update

~~~mermaid
sequenceDiagram
    participant D as Device
    participant O as Relay/Media
    participant L as LMS
    D->>O: Export request + installed release/model inventory
    O->>L: Import request
    L->>L: Resolve minimal delta bundle
    L-->>O: Signed release set + only missing artifacts
    O-->>D: Import package
    D->>D: Verify + preflight + stage + migrate + health-check
    alt Success
      D->>D: Commit
    else Failure
      D->>D: Rollback
    end
    D-->>O: Signed installation receipt
    O-->>L: Reconcile
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

## Device replacement / rehost

~~~mermaid
sequenceDiagram
    actor A as Authorized Admin
    participant O as Old Device
    participant N as New/Changed Device
    participant L as LMS
    A->>L: Submit replacement/rehost request
    N->>L: Register new cryptographic identity/fingerprint
    L->>L: Validate ownership + approval + allocation
    L->>L: Retire/suspend old binding
    L->>L: Reassign/return allocation
    L-->>N: New device-bound superseding grant
    N->>N: Verify and activate
    N-->>L: Acceptance receipt
~~~

## Device transfer

~~~mermaid
sequenceDiagram
    actor A as Requester
    actor B as Approver
    participant L as LMS
    participant D as Device
    A->>L: Request customer/site transfer
    L->>L: Validate current rights and target ownership
    L-->>B: Maker-checker approval request
    B->>L: Approve
    L->>L: Supersede invalid old grants + update ownership/site assignments
    L-->>D: New valid grant/policy state
    D-->>L: Acceptance receipt
~~~

## Revocation

~~~mermaid
sequenceDiagram
    actor A as Admin
    participant L as LMS
    participant D as Connected Device
    participant O as Air-gapped Device
    A->>L: Revoke grant/device
    L->>L: Record revocation + superseding state
    L-->>D: Deliver at sync/check-in
    D->>D: Enforce revoke
    Note over O,L: Air-gapped enforcement waits for signed import or offline expiry
~~~

## Failed update and rollback

~~~mermaid
sequenceDiagram
    participant L as LMS
    participant D as Update Manager
    participant R as Runtime
    L-->>D: Target release set
    D->>D: Verify + stage + install
    D->>R: Health check
    R-->>D: FAIL
    D->>D: Restore previous app/plugin/UI/model/config set
    D->>R: Verify rollback health
    alt Rollback healthy
      D-->>L: Rolled-back receipt
    else Rollback failed
      D-->>L: Critical failure receipt / escalate
    end
~~~

## Check-in freshness expiry

~~~mermaid
sequenceDiagram
    participant D as Device
    participant L as License Agent
    D->>L: Runtime authorization check
    L->>L: Compare last successful authorized check-in to policy
    alt Fresh
      L-->>D: Continue
    else Stale but grace/revalidation policy allows restricted state
      L-->>D: Restricted/grace + recovery path
    else Authorization no longer valid
      L-->>D: Disable unauthorized analytics
      Note over D,L: Preserve recovery and diagnostics where allowed
    end
~~~

## Commercial expiry and grace

~~~mermaid
sequenceDiagram
    participant R as Runtime
    participant L as License Agent
    R->>L: Feature authorization request
    L->>L: Evaluate commercial valid_until independently from offline freshness
    alt Commercial term active
      L-->>R: Allow subject to other gates
    else Expired and grace active
      L-->>R: Grace/restricted behavior per policy
    else Expired and grace ended
      L-->>R: Deny analytics execution
      Note over R,L: Keep recovery and diagnostics where allowed
    end
~~~