# Server-side systems

## Topology

- One image SHOULD serve every process type, with the role selected on the command line.
- Instances MUST be stateless and interchangeable, so that the platform can start and stop them at will.
- Administrative tasks MUST run as isolated instances of the app, with the same configuration, rather than by hand against production.

## Health checks

- A liveness check MUST NOT check a backing service, because a restart can't fix a dependency.
- A readiness check MAY check only what is local to the instance.
- A check of shared dependencies MAY be exposed for monitoring, but MUST NOT be able to restart the instance or take it out of rotation.

## Data

- Indices MUST be specified with the schema, including the uniqueness constraints that make retries safe and the expiry that enforces retention.
