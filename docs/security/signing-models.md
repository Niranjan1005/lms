# Signing & Model Protection

- Grants are digitally signed.
- Software/model manifests and artifacts are separately signed.
- License-signing and release-signing use separate key purposes.
- Private signing keys stay outside normal application storage.
- Devices verify using trusted public keys.
- Production should use managed KMS/HSM-backed custody or equivalent protected boundary where feasible.

Model baseline: entitlement-controlled, device-authorized decryption. Avoid one universal model password. Exact key wrapping and secure local key storage remain a Security ADR.