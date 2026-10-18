# Assisted-Offline Relay Security

The relay workstation/laptop is a transport convenience, never a licensing authority.

## Required properties

- no license or release signing private keys
- short-lived/operator-scoped authentication to the central LMS where connectivity exists
- encrypted local storage for staged request/response packages where feasible
- automatic cleanup/retention policy for staged packages
- no universal customer/device secrets
- package integrity preserved end-to-end; relay cannot modify signed content undetected
- audit of upload/download operator and request ID where possible

## Lost or compromised relay

Compromise of the relay should expose at most staged encrypted/signed package material and short-lived credentials, not signing authority. Replayed/stolen response packages remain bound to request ID, nonce and device identity.