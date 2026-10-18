# Backup Retention & Restore Validation

## Backup classes

- transactional PostgreSQL backups
- artifact repository backups/replication
- audit data backups
- configuration/reconstruction metadata
- signing-key recovery through its separate protected mechanism

## Proposed retention baseline

Retention must be finalized by operations/compliance, but the implementation should support daily/weekly/monthly policy tiers and customer-specific extensions.

## Restore validation

A backup is not considered reliable until restore is tested. Scheduled restore exercises verify:
- DB integrity and migration compatibility
- artifact hashes
- audit availability
- application startup
- customer/tenant access behavior
- signing integration restoration without exposing key material

## Evidence

Restore exercises record backup ID, environment, restore duration, validation checks, failures/exceptions and remediation owner.