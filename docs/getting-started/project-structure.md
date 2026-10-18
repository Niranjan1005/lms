# Project Structure & Standard Commands

## Recommended application repository shape

~~~text
lms/
├── backend/
│   ├── app/
│   ├── migrations/
│   └── tests/
├── portal/
│   ├── src/
│   └── tests/
├── edge/
│   ├── identity/
│   ├── license_agent/
│   ├── capacity/
│   ├── update_manager/
│   └── tests/
├── packaging/
├── scripts/
├── docs/
└── .github/workflows/
~~~

The handbook may remain in this repository or a dedicated docs repository, but code ownership and documentation links must remain traceable.

## Standard local services

- PostgreSQL
- artifact-storage emulator or local approved filesystem abstraction
- development signing provider using non-production keys
- backend API
- portal dev server
- optional local edge simulator/test agent

## Standard commands

Projects should expose consistent commands through Makefile/task runner/scripts, for example:

~~~text
make setup
make lint
make test
make test-integration
make migrate
make run-backend
make run-portal
make docs
make security-scan
~~~

Exact tooling may differ, but CI and developer commands should invoke the same underlying checks.

## Seed data

Development seed data should include synthetic customers, sites, devices, entitlements, grants, capacity profiles, marketplace features and release/model metadata so critical flows can be exercised locally without production data.