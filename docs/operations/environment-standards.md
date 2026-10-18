# Environment Standards

## Environment classes

| Environment | Purpose | Data rule | Release channels |
|---|---|---|---|
| Local Dev | developer iteration | synthetic only | Development |
| Integration | service/edge integration | synthetic/test | Development/QA |
| QA | formal validation | synthetic/anonymized | QA/Internal |
| Staging | production-like readiness | anonymized/approved | Internal/Stable candidate |
| Production | customer service | real customer data | Stable/LTS only |

## Separation requirements

- Separate credentials and secrets per environment.
- Production signing keys are never available in lower environments.
- Development/QA artifacts cannot be promoted implicitly into production; promotion creates explicit approved release state.
- Test tenants/devices are clearly marked.
- Production backups are not restored into lower environments without approved sanitization.

## Configuration

Configuration is supplied through environment/secret manager/deployment configuration, never hard-coded. Environment-specific settings include DB connection, artifact storage, signing provider, email provider, telemetry endpoints and auth mode.

## Time

All servers use reliable time synchronization. Persist timestamps in UTC. Site timezone is used for display and maintenance-window interpretation.