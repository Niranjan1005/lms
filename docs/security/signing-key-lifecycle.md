# Signing Key Rotation & Recovery

License-signing and release-signing keys have separate lifecycle and trust purpose.

## Key states

~~~text
GENERATED -> ACTIVE -> RETIRING -> RETIRED -> DESTROYED
~~~

Compromised keys may enter `REVOKED/COMPROMISED` through emergency procedure.

## Rotation

1. Generate new key in protected provider.
2. Distribute/ship new public verification key or trust bundle before first use.
3. Mark new key active for signing.
4. Keep old public key trusted for the planned verification window.
5. Stop issuing new artifacts with retiring key.
6. Retire old key after compatible clients have received trust updates.

## Recovery

Private-key recovery uses KMS/HSM/provider-specific protected mechanisms and is separated from normal database backup. Recovery exercises must not export raw private material unless the approved provider procedure explicitly requires a protected escrow mechanism.

## Compromise response

- stop signing with affected key immediately
- identify grants/releases signed with the key
- activate replacement key/trust bundle
- assess offline devices that may not receive trust updates immediately
- supersede/revoke affected artifacts where necessary
- preserve audit evidence and run security incident process

## Trust-store versioning

Edge verification components record trust-store version and key IDs so support can distinguish unknown-key failures from invalid signatures.