# ADR-010 — Release Package Format

**Status:** Proposed

## Baseline

Traditional release bundle with signed manifest, application/UI/dependency artifacts, automated migration, health-check and rollback handlers. Linux shell handlers are first; Windows PowerShell equivalents remain future-compatible.

## Decision required

Freeze archive/container format, canonical manifest serialization, compression, maximum package size, script execution sandboxing and artifact repository layout before Update Manager implementation is finalized.