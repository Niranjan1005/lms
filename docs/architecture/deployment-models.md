# Deployment Models

## SaaS

- Multi-tenant logical isolation.
- Phase 1: single-primary baseline with monitoring, automated backups and documented recovery.
- Design remains HA-ready.

## Customer-hosted

- Same LMS codebase.
- Isolated deployment.
- Manual LMS package upgrade acceptable initially.
- HA is optional enterprise capability.

## Delivery routes

1. Online API.
2. Assisted offline relay.
3. Fully air-gapped signed request/response.

All use the same signed artifact trust model.