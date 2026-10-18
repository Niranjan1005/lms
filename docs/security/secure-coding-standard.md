# Secure Coding Standard

This standard applies to backend, portal, edge agents, update tooling and offline package parsers.

## Input and parser safety

- Treat all external input as untrusted.
- Validate types, ranges, lengths and enum values.
- Reject unknown critical fields in signed/canonical payloads where ambiguity would be dangerous.
- Bound archive extraction size/file count.
- Prevent path traversal and symlink escape.
- Never execute unsigned scripts or packages.

## Authentication and authorization

- Authenticate before authorization.
- Enforce permission + scope at service/use-case boundaries.
- Never trust customer/site/device IDs supplied by clients without scope validation.
- No authorization logic only in UI.

## Cryptography

- Use approved libraries; do not implement custom primitives.
- Never log secret/private key material.
- Separate key purposes.
- Make signature verification fail closed.
- Verify signature before processing executable/decryptable artifact content wherever practical.

## Database

- Parameterized ORM/query usage only.
- Explicit transaction boundaries.
- Tenant/customer predicates in business queries.
- Migrations reviewed for destructive/locking impact.

## Logging

Log request ID, actor/object IDs and safe diagnostic context. Do not log passwords, tokens, private keys, raw license secrets, decrypted models or customer-sensitive payloads.

## Dependency security

Pin/constraint dependencies, scan for known vulnerabilities and maintain a documented upgrade/remediation process.