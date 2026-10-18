# Incident Response

Incident response covers security events and operational failures that materially affect licensing, tenant isolation, deployment, model protection or customer availability.

## Lifecycle

~~~text
Detect -> Triage -> Classify -> Contain -> Preserve Evidence -> Recover -> Validate -> Communicate -> Post-Incident Review
~~~

## Immediate evidence

Preserve:
- request/correlation IDs
- security/audit events
- affected tenant/customer/device IDs
- deployment job/target history
- relevant application/security/edge logs
- artifact/release hashes and manifest IDs
- grant revisions
- signing/trust key IDs (never raw private key material)
- timestamps and operator actions
- relevant approval records

## Containment rule

Containment must avoid destroying evidence or making unsafe commercial changes. Do not bypass signature/tenant controls merely to restore service.

## High-priority playbooks

### Suspected signing-key compromise

1. stop new signing with affected key
2. identify signed grants/releases and potential exposure window
3. activate approved replacement key where available
4. distribute trust-bundle update through supported routes
5. assess air-gapped devices that cannot receive immediate trust changes
6. supersede/revoke affected artifacts/grants where policy requires
7. validate restored signing and initiate post-incident review

### Tenant-isolation incident

1. treat as security-critical until disproven
2. restrict risky support/global access paths
3. preserve request/query/audit evidence
4. identify data read/write exposure and affected tenants
5. remediate authorization/query defect
6. add regression tests before reopening path
7. follow legal/customer notification policy where applicable

### Artifact repository compromise / tampered release

1. stop affected deployments
2. block suspect release/artifact identities
3. verify signed manifest/content hashes from trusted build evidence
4. rotate repository credentials if compromised
5. rebuild/re-publish as a new release if needed
6. inspect devices that received suspect content
7. use rollback where active release is unsafe

### Model key / wrapping compromise

1. disable affected wrapping/master-key path
2. identify model releases and wrapped-key scopes
3. rotate KEK/wrapping configuration using approved provider process
4. regenerate wrapped keys/release metadata as required
5. assess offline devices unable to receive replacement authorization
6. document IP/data exposure assessment

### Compromised human credential / privileged account

1. revoke sessions/tokens
2. disable/reset identity through IdP/auth system
3. review privileged actions/audit exports
4. rotate any derived secrets exposed by the account
5. restore access using approved identity recovery
6. review role assignments and strengthen controls if needed

### Widespread bad release

1. stop/pause rollout
2. mark release blocked
3. rollback to known-good release set
4. verify rollback health receipts
5. preserve failed installation evidence
6. communicate affected customers according to incident policy

### Malicious/malformed offline package exploit attempt

1. quarantine media/package
2. preserve package hash and parser error evidence
3. determine whether parsing occurred before signature verification
4. block/revoke package/request identity as appropriate
5. patch parser and add regression/fuzz case
6. inspect similarly exposed devices

## Communications

External communications contain confirmed impact, affected scope and recovery guidance only. Unvalidated technical hypotheses and sensitive security details remain internal until approved.

## Closure criteria

Incident is closed only after containment, recovery validation, evidence retention, customer/internal communications, root-cause analysis, corrective actions with owners and regression/monitoring improvements are documented.