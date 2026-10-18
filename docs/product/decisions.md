# Approved Decisions

| Decision | Baseline |
|---|---|
| Backend | Python 3.12 + FastAPI modular monolith |
| Database | PostgreSQL + SQLAlchemy + Alembic |
| Admin UI | React + Vite + TypeScript |
| Deployment | SaaS and customer-hosted |
| OS | Ubuntu/Linux first; future Windows-compatible abstractions |
| Development auth | Username/password; production IAM later ADR |
| Trial | Default 7 days, configurable; starts at first successful feature activation |
| Offline validity | Default 7 days, hierarchical override |
| Grace | Default 7 days, independently configurable |
| Add-ons | Normally co-terminate with subscription base |
| Capacity | Recommend; never silently alter purchased rights |
| Packaging | Traditional signed release bundles; no Docker dependency |
| Auto OTA | Supported; Stable channel by default |
| Maintenance window | Default 01:00–03:00; customer configurable |
| Rollback | Keep 2–3 known-good versions where disk permits |
| Model OTA | Independent, encrypted, signed and rollback-capable |
| Audit retention | Configurable; baseline 1–3 years |
| ERP | Separate system with synchronization interfaces |