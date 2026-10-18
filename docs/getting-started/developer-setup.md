# Developer Setup

This page defines the baseline local development workflow for the LMS handbook and the future application repositories.

## Required tools

- Python 3.12
- Git
- PostgreSQL client/server for backend development
- Node.js LTS for React/Vite portal development
- MkDocs dependencies from `requirements.txt` for handbook work

## Handbook preview

~~~bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
mkdocs serve
~~~

## Development principles

- Use synthetic data only.
- Never use production signing keys in development.
- Keep configuration outside source code.
- Run migrations through Alembic only.
- Use feature flags/policy configuration rather than ad-hoc code branches for customer exceptions.
- Keep edge interfaces backward-compatible across supported release windows.

## Before opening a PR

- run unit/integration tests for affected code
- run `mkdocs build --strict` for documentation changes
- update ADRs when architecture changed
- verify no secrets/customer data are included
- document rollback/migration impact