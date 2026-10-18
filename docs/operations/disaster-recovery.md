# Disaster Recovery & Continuity

Phase 1 remains operationally simple but recovery is designed before production.

## Proposed recovery tiers

| Component | Baseline approach |
|---|---|
| PostgreSQL | automated encrypted backups + tested restore |
| Artifact repository | versioned/replicated object storage or protected backup |
| Audit data | protected backup; append-only semantics |
| Signing metadata | database backup; private keys handled separately |
| Signing keys | KMS/HSM/provider-specific protected recovery |
| Customer-hosted LMS | documented manual restore package/process |

## RTO/RPO

Exact enterprise RTO/RPO remain an open business/operations decision. Until approved, no team should promise contractual recovery targets.

## Mandatory DR testing

- scheduled restore test
- database migration + restore compatibility test
- artifact integrity verification
- signing-key recovery procedure exercise without exposing key material
- documentation of measured restore time and exceptions