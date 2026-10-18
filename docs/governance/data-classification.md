# Data Classification & Handling

Classification determines where LMS information may be stored, logged, exported and shared. Classification applies to documents, database fields, logs, backups, support bundles and offline packages.

## Classes

| Class | Examples | Handling baseline |
|---|---|---|
| Public | approved public product material | externally shareable after publication approval |
| Internal | architecture, roadmaps, non-customer operational metrics | company/internal authorized access |
| Confidential | customer/device inventories, entitlement details, audit exports, deployment metadata | need-to-know, scoped access, encrypted transport/storage controls |
| Highly Restricted | signing private keys, passwords/tokens, model content keys, security incident secrets | dedicated protected systems; never normal docs/logs/tickets |

## Default classification examples

- customer/site/device topology: Confidential
- entitlement/allocation/grant metadata: Confidential
- signed grant artifact: Confidential unless product policy classifies differently
- audit/security export: Confidential
- source architecture handbook: Internal
- model binary/IP: Confidential or Highly Restricted according to owner policy
- private signing key / KEK / unwrapped DEK: Highly Restricted
- authentication token/password: Highly Restricted

## Storage rules

Highly Restricted key/credential material is stored only in approved key/secret systems and is never copied into PostgreSQL business tables, documentation or ordinary support archives.

Confidential data in PostgreSQL/artifact storage/backups uses deployment-appropriate access control and encryption-at-rest capabilities.

## Logging

Logs prefer identifiers/references over full payloads. Highly Restricted values are always redacted. Confidential payload details are logged only when explicitly justified in an approved secure diagnostic path.

## Export and support bundles

Exports enforce tenant/object scope. Sensitive global exports may require privileged approval. Support bundles must minimize data and exclude secrets/private keys/decrypted model material.

## Lower-environment data

Production customer data/backups are not copied into development/QA by default. Any approved lower-environment use requires sanitization/anonymization appropriate to classification.

## Retention/deletion

Retention follows audit/business/compliance policy by data class. Legal/security hold overrides normal deletion. Backup copies follow their own managed retention lifecycle.

## Incident rule

Suspected unauthorized disclosure of Confidential or Highly Restricted information triggers security incident triage according to impact and scope.