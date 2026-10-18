# Data Classification & Handling

## Classes

| Class | Examples | Handling baseline |
|---|---|---|
| Public | approved public product docs | may be shared externally |
| Internal | architecture, roadmaps, operational metrics | company/internal access |
| Confidential | customer/device inventories, entitlement details, audit exports | restricted need-to-know |
| Highly Restricted | signing private keys, credentials, model content keys, incident secrets | dedicated protected systems; never normal docs/logs |

## Repository rule

This private handbook may contain Internal and selected Confidential design information, but never secrets, credentials, private keys, decrypted proprietary models or raw sensitive incident/customer exports.

## Logging rule

Logs should contain identifiers and references, not full sensitive payloads unless explicitly approved for a secure diagnostic channel.

## Export rule

Audit/report exports must enforce caller scope and may require additional approval depending on customer data sensitivity.