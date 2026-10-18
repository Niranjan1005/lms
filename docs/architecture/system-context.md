# System Context & External Boundaries

~~~mermaid
flowchart LR
    VA[Vendor Admin / Support / Release] --> LMS[LMS Control Plane]
    CA[Customer / Site Admin] --> LMS
    ERP[ERP / Billing] <--> LMS
    IDP[Future OIDC / SSO IdP] --> LMS
    SMTP[Email / Notification Provider] <--> LMS
    STORE[(Artifact Repository)] <--> LMS
    KMS[Protected Signing / KMS-HSM] <--> LMS
    LMS <--> EDGE[Edge Devices / Servers]
    RELAY[Authorized Offline Relay] <--> LMS
    RELAY <--> EDGE
    LMS --> OBS[Monitoring / Logs / Audit Export]
~~~

## Ownership boundaries

- LMS owns operational entitlement, grant, deployment, capacity and lifecycle state.
- ERP owns financial/order truth when integrated.
- Signing provider owns protected private-key operations.
- Artifact repository stores immutable release/model binaries, not commercial truth.
- Edge owns final local license verification, actual runtime capacity validation and installation commit/rollback.
- Relay transports signed packages and has no issuance authority.

## Trust boundaries

Human portal sessions, device cryptographic identity, signing infrastructure, artifact storage and offline media are separate trust zones. Data crossing each boundary is authenticated, authorized and validated according to the relevant security section.

## Failure-domain principle

Loss of a non-critical external dependency should not silently corrupt licensing state. Email failure must not undo a renewal; telemetry failure must not invalidate a license; artifact-store failure must not mutate entitlement; signing failure queues/retries issuance rather than producing unsigned grants.