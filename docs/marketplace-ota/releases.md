# Release Management

## Channels

~~~text
Development -> QA -> Beta/Internal -> Stable -> LTS -> Retired
~~~

Automatic production updates consume Stable by default. LTS targeting is explicitly controlled by the company.

## Traditional package standard

~~~text
release/
├── manifest.json
├── application/
├── ui/
├── migrations/
├── configs/
├── dependencies/
├── install/
│   ├── install.sh
│   ├── rollback.sh
│   └── healthcheck.sh
└── signature
~~~

No manual site migration should be required in normal releases.