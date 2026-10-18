# Developer Setup

This page defines the local baseline for handbook work and future LMS application development. Exact application commands become executable once the implementation scaffold exists; environment/security rules apply now.

## Required tools

- Git
- Python 3.12
- PostgreSQL client/server or approved local container for development
- Node.js LTS for React/Vite portal
- MkDocs dependencies from `requirements.txt`
- optional Make/task runner once application scaffold is created

## Clone and handbook preview

~~~bash
git clone <repository>
cd lms
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
mkdocs serve
~~~

Documentation changes must pass:
~~~bash
mkdocs build --strict
~~~

## Local application dependencies

When backend implementation begins, local development should provide:
- PostgreSQL
- development-only signing provider/key
- local artifact repository adapter
- backend API
- worker/scheduler
- portal dev server
- optional edge simulator/agent

## Configuration

Use environment/development config files excluded from source control or approved local secret tooling. Never hard-code DB passwords, signing keys, tokens or customer credentials.

## Data

Use synthetic seed data only: customers, sites, devices, entitlements, allocations, grants, capacity profiles, features, releases/models and deployment state. Production exports/backups are prohibited unless formally sanitized/approved.

## Cryptography

Development uses isolated non-production keys. Production KMS/HSM keys and model KEKs are never available in local developer environments.

## Database workflow

- create schema through Alembic
- do not manually patch local schema and then forget migration
- use disposable local DB for destructive development experimentation
- test upgrade/downgrade/forward compatibility according to migration policy

## Before PR

- sync/rebase from current main according to team policy
- run lint/type/unit/integration checks for affected code
- run migration tests for schema changes
- run `mkdocs build --strict` for docs changes
- verify no secrets/customer data/binary proprietary releases are committed
- update SDR/ADR/handbook when behavior or architecture changes
- document rollback/compatibility impact

## Security hygiene

Do not disable certificate/signature/tenant checks in production code paths to make local development easier. Development bypasses, if unavoidable, are explicit environment-scoped implementations that cannot be enabled accidentally in production.