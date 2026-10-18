# Backup & Recovery

Back up PostgreSQL state, audit data, artifact metadata, release manifests, artifact repository and reconstruction configuration.

Signing private keys use a separate protected backup/recovery process and are never handled as normal database backup material.

Phase 1 SaaS baseline: single primary + automated backups + monitoring + documented recovery, while remaining HA-ready.