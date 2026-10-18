# Trust Boundaries

The LMS has multiple trust zones. Security decisions must be based on which boundary data crosses, not only whether a request is 'internal'.

## Trust zones

| Zone | Trusted for | Not trusted for |
|---|---|---|
| Human browser/session | authenticated user intent after authn/authz | tenant/object authority without server checks |
| LMS application | business policy/orchestration | production signing private-key custody |
| PostgreSQL | transactional state | signing authority or executable artifact trust |
| Artifact repository | immutable artifact storage | deciding entitlement or execution rights |
| Signing service/KMS/HSM | protected cryptographic operations | commercial policy decisions |
| Edge device | local enforcement/actual runtime evidence | central commercial truth |
| Offline relay/media | transport only | signing, entitlement or device authority |
| ERP | commercial/order truth where integrated | device grant/runtime truth |

## Central boundary

Commercial authorization is evaluated centrally. The application sends an authorized signing request to the protected signing boundary; it never loads raw production signing private keys.

## Edge boundary

The edge verifies signature, key trust, subject binding, commercial term, revision/supersession, dependencies, offline freshness/grace, package/model integrity, compatibility and local capacity before execution.

## Offline boundary

Offline request/response packages must be safe even if the relay/media is untrusted.

~~~mermaid
sequenceDiagram
    participant D as Device
    participant R as Relay / Media
    participant L as LMS
    participant S as Signing Service
    D->>D: Generate request_id + nonce + signed request
    D->>R: Export request
    R->>L: Transport only
    L->>L: Validate tenant/device/policy/replay
    L->>S: Authorized signing request
    S-->>L: Signed grant/manifest
    L-->>R: Device-bound response package
    R-->>D: Controlled-media transfer
    D->>D: Verify signature/hash/request binding/revision
    D->>D: Local capacity + install/health
    D-->>R: Signed receipt
~~~

## Boundary rules

- every cross-zone input is authenticated/validated according to its trust source
- object IDs are not authorization
- artifact location is not proof of integrity
- relay possession is not proof of device authorization
- database possession is not signing authority
- local device reports are evidence and may be stale/tampered on a compromised host
- telemetry failure does not alter commercial entitlement
- email/notification failure does not roll back business transactions

## Failure containment

External dependency failures use transactional outbox/retry rather than corrupting commercial state. Signing outage blocks new signed issuance but does not invalidate already valid grants. Artifact outage blocks delivery, not entitlement. ERP outage delays reconciliation, not local device enforcement.