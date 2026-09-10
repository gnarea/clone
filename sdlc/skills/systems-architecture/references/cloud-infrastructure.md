# Cloud infrastructure

Infrastructure is published, so a coerced change is a public change. It MUST therefore read as an argument that an outsider can check, not as a pile of resources.

## Provisioning

- Every resource MUST be declared as code, in a repository, and applied from there. Anything provisioned by hand MUST be named in the repository's documentation, with the reason and the ticket tracking its removal.
- Configuration that recurs across estates (e.g., repository settings, or an alerting channel) MUST be a shared, versioned module, pinned by version at each call site.
- Files MUST be partitioned by domain (e.g., `kms`, `iam`, `network`, `billing`, `alerts`), never by construct type.
- A body of infrastructure with a known end date (e.g., resources supporting an audit) MUST be confined to its own deletable file, declaring its own variables.
- Continuous integration MUST validate; it MUST NOT plan or apply. Applying MUST require a human act, and promotion to production MUST be a change in a separate file or repository from the one that built the artefact.

## Least privilege

- Each workload MUST have its own identity, and MUST be granted the narrowest permission set that lets it work. Permissions SHOULD be enumerated one by one rather than taken wholesale from a predefined role.
- Where the provider supports conditional grants, access MUST be constrained by resource, not only by role.
- A service that no external client needs to reach MUST be unreachable from the public Internet, rather than merely unadvertised.
- Human access to production MUST be exceptional. Servers SHOULD be immutable, and interactive access SHOULD NOT be available at all.
- A workload SHOULD obtain its credentials from the platform's identity service, rather than from a stored secret.

## Cost

- Every estate MUST declare a budget, with alerts on both actual and forecast spend, routed to a channel whose name identifies the estate it belongs to.

## Defence in depth

- Mitigations MUST be layered by who is best placed to bear them: volumetric attacks to the hosting provider, protocol-level attacks to a mainstream reverse proxy, and application-level attacks to our own code.
