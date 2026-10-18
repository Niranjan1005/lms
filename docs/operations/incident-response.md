# Incident Response

Incident response covers security events and operational failures that materially affect licensing, deployment, model protection or customer availability.

## Lifecycle

~~~text
Detect -> Triage -> Contain -> Recover -> Validate -> Communicate -> Post-incident review
~~~

## Immediate evidence

Preserve:
- request/correlation IDs
- audit events
- deployment job/target history
- relevant application/security logs
- artifact/release hashes
- grant revisions
- signing key IDs (never private key material)
- timestamps and operator actions

## High-priority scenarios

### Suspected signing-key compromise

1. stop new signing using affected key
2. activate approved replacement key if available
3. identify artifacts/grants signed by impacted key
4. assess online/offline blast radius
5. distribute trust/key-rotation update using approved path
6. revoke/supersede affected grants/artifacts where required
7. initiate security incident and post-incident review

### Widespread bad release

1. stop rollout/concurrency queue
2. mark release blocked
3. trigger rollback to known-good release set
4. verify health receipts
5. preserve failed installation evidence
6. communicate affected customers

### Tenant-isolation suspicion

Treat as security-critical until disproven. Freeze risky admin actions, preserve evidence, scope affected data and escalate immediately.

## Communications

External communications contain confirmed impact and recovery guidance only. Technical hypotheses and sensitive security details remain internal until validated.