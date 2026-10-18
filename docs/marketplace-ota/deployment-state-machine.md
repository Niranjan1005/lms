# Deployment Job State Machine

Deployment orchestration must be restart-safe and deterministic.

## Job states

~~~mermaid
stateDiagram-v2
    [*] --> Draft
    Draft --> Scheduled
    Scheduled --> Running
    Running --> Completed
    Running --> PartiallyFailed
    Running --> Failed
    Scheduled --> Cancelled
    Running --> Cancelling
    Cancelling --> Cancelled
~~~

## Target states

~~~mermaid
stateDiagram-v2
    [*] --> Pending
    Pending --> WaitingWindow
    WaitingWindow --> Preflight
    Preflight --> Downloading
    Downloading --> Verifying
    Verifying --> Staging
    Staging --> Installing
    Installing --> HealthCheck
    HealthCheck --> Active
    HealthCheck --> RollingBack
    RollingBack --> RolledBack
    Preflight --> Blocked
    Verifying --> Failed
    Installing --> Failed
~~~

## Retry policy

- Network/artifact transient failures may retry with exponential backoff.
- Signature/hash/compatibility failures are non-retryable until input changes.
- Installation failure triggers rollback before retry consideration.
- Automatic mode obeys maintenance window and concurrency limits.
- Manual mode requires explicit deployment approval/start.

## Completion semantics

A job is `Completed` only when every target reaches Active or an explicitly accepted terminal exclusion state. `PartiallyFailed` preserves successful targets and clearly reports failed/rolled-back targets.