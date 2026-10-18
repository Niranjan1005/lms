# Trust Boundaries

## Central

Commercial authorization is central, but signing private keys are outside normal application storage.

## Edge

The edge verifies signature, binding, dates, revision, dependencies, offline freshness, package/model integrity and local capacity.

## Assisted offline

The relay is transport-only and has no signing authority.

~~~mermaid
sequenceDiagram
    participant D as Device
    participant R as Relay
    participant L as LMS
    participant S as Signing Service
    D->>R: Signed request + nonce
    R->>L: Upload request
    L->>S: Authorize and sign
    S-->>L: Signed grant / bundle manifest
    L-->>R: Response package
    R-->>D: Controlled-media transfer
    D->>D: Verify, install, activate
~~~