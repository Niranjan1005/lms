# Assisted-Offline Relay Security

The relay workstation/laptop moves signed request/response packages between isolated devices and LMS. It is an untrusted transport convenience, never a licensing, signing or entitlement authority.

## Threat assumptions

The relay may be lost, stolen, infected, shared between operators, connected to untrusted networks, or used to replay old package files. Security therefore relies on end-to-end device/central signatures and request binding rather than trusting the relay host.

## Required properties

- no license/release/model signing private keys
- no long-lived universal customer/device secret
- short-lived/operator-scoped central authentication where connected
- least-privilege access to download/upload only the requests/responses operator is authorized to handle
- encrypted local staging where platform permits
- automatic staging cleanup/retention
- package filenames/UI metadata are never trusted instead of signed payload identity
- upload/download actions logged with operator, customer/device/request IDs
- relay never edits/repackages signed payloads

## Request transport

Relay upload path SHALL preserve request bytes. LMS validates device signature, request ID, nonce, ownership, request age and replay state before producing any response.

## Response transport

Response is bound to device + request ID + nonce. Theft of a response should not make it usable on another device or for a new request.

## Local staging

- stage under per-request directories
- restrict filesystem permissions
- never auto-execute imported files
- scan/validate file type/size before central upload where possible
- securely delete or expire packages after configured retention
- avoid retaining decrypted model/application content; relay transports encrypted/signed artifacts

## Lost/compromised relay

Expected blast radius is limited to staged signed/encrypted package material and short-lived credentials. Response replay remains rejected by device request/revision state. On suspected compromise: revoke relay/operator session, rotate exposed integration credentials, review audit history and invalidate pending workflow material where practical.

## Air-gap media

When removable media replaces a relay application, the same signed request/response protocol applies. Operator procedure should use controlled media, malware scanning where available and clean staging systems, but media possession still grants no signing authority.

## Related SDR

`SDR-OFF-003` through `SDR-OFF-009`, `SDR-SEC-005`, `SDR-SEC-010`