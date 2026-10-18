# Support Escalation Model

## L1 — Operations / Support

Handles known runbooks, customer/site/device lookup, entitlement/grant status checks, offline package validation and standard rehost/renewal coordination.

## L2 — Engineering

Engaged for reproducible product defects, migration/update failures, capacity anomalies, integration issues and unsupported states not resolved by runbook.

## L3 — Architecture / Security / Release

Engaged for signing/key incidents, tenant isolation, systemic release failures, data integrity risk, cross-module design defects and emergency architecture decisions.

## Escalation packet

Every escalation includes:
- customer/site/device IDs
- request/correlation ID
- error code
- timestamps/timezone
- current grant/release/model revisions
- deployment/installation receipt state
- relevant safe logs
- steps already attempted
- business/customer impact

Avoid sending secrets or decrypted model material through ordinary support channels.