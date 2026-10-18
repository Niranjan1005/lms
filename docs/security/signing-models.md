# Signing, Cryptographic Trust & Model Protection

## Key-purpose separation

At minimum, use separate key purposes for:

1. license/grant signing
2. application/release manifest signing
3. model/package signing if separated operationally
4. model content-encryption key wrapping/master-key operations
5. device identity keys

A single universal private key must not perform all trust functions.

## Grant signing flow

~~~mermaid
sequenceDiagram
    participant LMS as LMS Grant Service
    participant POL as Policy/Entitlement
    participant SIG as Protected License Signer
    participant D as Device License Agent
    LMS->>POL: Resolve approved grant payload
    POL-->>LMS: Canonical grant fields
    LMS->>SIG: Authorized signing request + canonical bytes/hash
    SIG-->>LMS: key_id + algorithm + signature
    LMS-->>D: Signed grant
    D->>D: Rebuild canonical bytes and verify signature
~~~

The LMS stores signing metadata and signed output; raw signing private key material never enters application/database storage.

## Release signing

Release and model manifests are immutable after publication. Edge verifies manifest schema/version, release-signing key trust, manifest signature, artifact content hash, artifact signature if the artifact format carries one, and target compatibility.

No package is executed merely because it came from the artifact repository.

## Cryptographic algorithm baseline

Ed25519 is the preferred initial signature algorithm where required platforms/providers support it. Final algorithm/provider support remains subject to security and compatibility review. SHA-256 or stronger is used for content integrity unless an approved profile replaces it.

Algorithm and canonicalization profile are versioned in signed objects so future migration is possible.

## Model encryption

Model binaries are encrypted independently from license grants. Entitlement answers whether a device may use a model; the encryption system determines whether an authorized device/deployment can obtain the content key.

~~~text
Random per-artifact DEK
        ↓ encrypts
Encrypted model artifact
        ↓
DEK wrapped by protected KEK / device-deployment authorization
        ↓
Authorized edge unwrap path
~~~

## Model key handling requirements

- DEKs generated with a CSPRNG
- plaintext DEKs not stored in normal LMS DB/logs
- wrapped-key metadata records model release, key version and authorized scope
- decryption authorization tied to valid device/deployment context
- plaintext model exposure minimized on edge
- temporary/cache plaintext handling defined by edge implementation
- revocation cannot guarantee remote deletion on a hostile fully offline/root-compromised host; it prevents legitimate future authorization/use according to policy

A universal embedded password or customer-wide static decryption secret is prohibited.

## Trust-store management

Devices retain a versioned trust bundle with current and retiring verification public keys. Unknown key ID, invalid signature or revoked trust key is a hard verification failure.

## Open security decision

Exact model key hierarchy, KMS/HSM integration, per-device vs per-deployment key wrapping, local secure-storage facility and rotation cadence remain ADR-009 and must be resolved before production model-key implementation is frozen.