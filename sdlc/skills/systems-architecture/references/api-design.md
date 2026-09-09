# Contracts others depend on

A contract outlives every implementation behind it, and constrains everyone who has already built against it, so the investment goes into the surface rather than into what sits behind it.

## Surface

- The published surface MUST be the smallest one that serves the use case. Everything else MUST be unreachable, rather than undocumented.
- The core of the contract MUST be specified independently of any transport, vendor, or runtime it runs on today.
- A security-relevant choice MUST NOT be delegated to the caller, and an unsafe option MUST be inexpressible rather than discouraged.

## Extension

- Extension MUST happen through a named extension point (e.g., a binding, a registry, or a profile), specified separately from the core. An extension MAY add to the core, but MUST NOT override it.
- The extension point MUST exist before the first extension does, and a new capability MUST arrive as an extension rather than as a revision of the core.
- Where a new use case is a narrowing of an existing contract rather than an addition to it (e.g., mandating a subset, or a shorter validity period), it MUST be specified as a constraint on the original, adding no new mechanism.
- Versioning MUST be designed in from the first release, and MUST be carried by the contract's own identifiers.

## Failures

- Every failure that the other side must act on MUST have a stable identifier, and MUST be distinguishable by fault: what the caller sent, what we did, and what the infrastructure did.

## Documentation

- The contract MUST state its non-goals, and SHOULD state which gaps we would accept contributions for.
- Known limitations MUST be documented as limitations, in plain language, including where there is no workaround.
