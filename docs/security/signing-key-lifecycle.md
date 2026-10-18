# Signing Key Rotation & Recovery

License-signing and release-signing keys are separate trust purposes with independently auditable lifecycle. Model KEKs/wrapping keys follow their own security design but use the same governance principles.

## Key states
~~~text
GENERATED -> VALIDATED -> ACTIVE -> RETIRING -> RETIRED -> DESTROYED
                         |
                         +-> COMPROMISED / REVOKED
~~~

## Key metadata

Track key ID, purpose, algorithm, provider reference, created/activated/retiring/retired timestamps, status, owner, trust-bundle version and approval references. Raw private key material is not stored in LMS metadata.

## Generation

Production key generation occurs inside KMS/HSM/equivalent protected provider using approved algorithm/profile. Creation and activation are distinct actions where provider/process permits.

## Rotation

1. generate/validate new key
2. publish/distribute new public verification key in trust bundle
3. confirm supported online/offline edge versions can trust it
4. maker-checker activate new signing key
5. stop new issuance with old key; mark Retiring
6. retain old public key for verification overlap
7. retire old key after planned artifact/grant/support window
8. eventually destroy private key according to retention/compliance policy

## Trust-bundle distribution

Trust bundle is versioned and itself delivered through an authenticated/signed update path. Devices report trust-bundle version/key IDs so support can distinguish unknown-key from invalid-signature failures.

## Offline considerations

Air-gapped devices may miss rotation updates. Rotation plan therefore accounts for overlap long enough to distribute trust state through offline packages, or uses a controlled compatibility/recovery path. Emergency compromise may require stricter blocking despite offline impact.

## Recovery

Private-key recovery uses provider-specific protected backup/replication/escrow mechanisms. It is separate from normal DB backup. Recovery drills verify operational procedure without exporting raw key material into ordinary files.

## Compromise response

- stop signing with affected key
- mark key compromised/revoked in central trust policy
- identify grants/releases signed during exposure window
- activate replacement key
- distribute updated trust bundle
- supersede/revoke/reissue affected artifacts where required
- assess offline devices and support impact
- preserve evidence and run Security incident process

## Algorithm migration

Signed artifacts carry algorithm and key ID. Introducing a new algorithm uses a versioned overlap/migration plan rather than silently changing verification semantics.

## Separation of duties

Key activation/rotation/revocation is privileged, maker-checker controlled and audited. Application administrators do not automatically gain KMS/HSM key-administration rights.

## Related SDR/ADR

`SDR-SEC-003`, `SDR-SEC-004`; ADR-006