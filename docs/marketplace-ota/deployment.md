# Deployment & Rollback

Policy hierarchy:

~~~text
Platform Default -> Customer Policy -> Site Policy -> Device Override
~~~

Supported settings include AUTO/MANUAL, channel, maintenance window, model-only OTA, application OTA, concurrency and auto-rollback.

Default automatic maintenance window: 01:00–03:00, customer configurable.

Rollback restores a coherent release set, not only one binary. Keep 2–3 known-good releases when disk permits; always preserve at least the immediately previous known-good version.