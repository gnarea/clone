# Server-side systems

## Topology

- One image SHOULD serve every process type, with the role selected by the command line, and the documentation MUST tell operators not to override the command.
- Instances MUST be stateless and interchangeable, so that the platform can start and stop them at will.
- A background worker SHOULD be an HTTP server that accepts posted work and answers with a status code, rather than a client of a particular broker, so that the broker stays the operator's choice.
- Administrative and maintenance tasks MUST run as isolated instances of the app, with the same configuration, rather than by hand against the production data store.

## Health checks

- A liveness check MUST NOT reach for a backing service, because a failed one restarts the process, and a restart cannot fix a dependency. Where the platform offers only one probe, that probe MUST be this one.
- A readiness check MAY probe what the instance needs in order to serve, but MUST NOT fail on a dependency shared by every instance, because that turns a degraded service into an unreachable one.
- A check that does probe dependencies MAY be exposed for operators and monitoring, but MUST NOT be wired to anything that can restart the process or take it out of rotation.

## Data

- The system MUST persist as little as it can, and every collection MUST have a retention rule enforced by the store.
- Indexes MUST be treated as part of the design: the uniqueness constraints that make retries safe, and the expiry indexes that implement retention, MUST be specified with the schema rather than added operationally.
- A record that guards against duplicate processing MUST expire exactly when the work it guards can no longer arrive.
- A write MUST NOT be preceded by a check for an existing record, because two matching requests can arrive at once.
