# Edge Host Hardening Baseline

Edge controls assume the device may be intermittently connected and physically accessible. The goal is to reduce attack surface and protect legitimate operation; software alone cannot guarantee security against an attacker with persistent root/administrator control.

## Service isolation

- run LMS edge agents/runtime as dedicated least-privilege service accounts where practical
- restrict writable directories
- separate update staging from active runtime paths
- local management APIs bind to loopback/local IPC by default
- firewall/network exposure is minimal and documented

## Key/state storage

- device private key uses TPM/secure element/OS keystore where available; otherwise strongest practical protected filesystem/keyring
- grant anti-rollback state and trusted time are stored with integrity protection where feasible
- normal users cannot modify active grant/release state
- backup/export processes do not copy raw private keys by default

## Update execution

- signature/hash verification before install
- install scripts are signed artifacts referenced by manifest
- scripts run with only required privilege
- staging directory is non-authoritative until health check commits
- rollback restores coherent known-good app/model/config state

## Logging

Edge logs avoid secrets and decrypted model data. Security-relevant failures include safe reason code, key ID/trust-bundle version and request/package identifiers.

## Host maintenance

Supported OS/runtime versions and security-patch expectations are part of compatibility policy. Unsupported/vulnerable runtime dependencies may block future releases according to product/security policy.

## Physical/root compromise limitation

An attacker with root may observe runtime memory or alter binaries outside the intended trust model. Cryptographic signing prevents legitimate software from accepting forged central authorization, but it cannot prove a hostile root-owned host is executing unmodified code without additional hardware attestation.