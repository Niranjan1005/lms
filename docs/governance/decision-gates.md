# Engineering Decision Gates

Large work items pass explicit decision gates before production.

## Gate 0 — Problem/Sponsor

Business outcome, owner, scope and success criteria approved.

## Gate 1 — Architecture Ready

Trust boundaries, state model, data ownership, APIs and ADR impact reviewed.

## Gate 2 — Development Ready

Stories, acceptance criteria, dependencies, test approach and environment needs are ready.

## Gate 3 — Release Candidate

Code complete, migrations/upgrades/rollback tested, security scans complete, docs current.

## Gate 4 — Production Approval

QA evidence, release notes, known issues, VAPT/security disposition, rollout/rollback plan and approvals complete.

## Gate 5 — Post-Release

Deployment health, incidents, customer feedback, metrics and follow-up actions reviewed.

Gate evidence should be traceable to issues/PRs/releases rather than captured only in meetings.