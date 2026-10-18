# LMS Engineering Handbook

Internal Tier-1 engineering handbook for the License, Marketplace & Edge Lifecycle Management Platform.

This repository is the engineering source of truth for architecture, licensing, Marketplace/OTA, model lifecycle, backend, edge/application, security, QA, operations, ADRs and delivery readiness.

## Local preview

~~~bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
mkdocs serve
~~~

## Governance

- Approved architecture belongs in this repository.
- Material design decisions require ADRs.
- Behaviour-changing code changes update the handbook in the same pull request.
- Proposed rules are labelled until approved.
- Security-sensitive operational details remain private.