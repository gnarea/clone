# Prototyping

A prototype exists to answer its questions as quickly as possible, so it gives up whatever only matters to a system that lasts. Before you design one, you MUST load the `prototyping` skill and follow it.

Every rule in this skill applies, except as follows.

- The design MUST cover only what the questions depend on. A component, a backing service, or an exchange that is already known to work MAY be left out, even where production couldn't do without it (e.g., authentication, encryption).
- The design MAY be documented in whatever form is quickest: the prototype needs no architecture document, threat model, or change spec of its own.
- Whatever only serves a system that lasts MAY be left out: retries, dead-lettering, degraded operation, scaling, alerting, backups, and the versioning and compatibility of contracts. Telemetry is needed only for what the questions measure.
- Infrastructure MAY be provisioned by hand.
