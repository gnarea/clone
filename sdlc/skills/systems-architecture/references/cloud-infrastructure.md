# Cloud infrastructure

## Provisioning

- Every resource MUST be declared as code and applied from a repository. Anything provisioned by hand MUST have tracked work to codify or remove it.
- Infrastructure code MUST be partitioned by domain (e.g., `iam`, `network`, `alerts`), never by construct type.
- Continuous integration MUST validate the code, but MUST NOT apply it. Applying MUST be a human act.
- Promotion to production MUST be a deliberate act, separate from merging or building.

## Least privilege

- Each workload MUST have its own identity, granted only the permissions it uses, enumerated rather than taken wholesale from a predefined role.
- Where the provider supports conditional grants, access MUST be constrained by resource, not only by role.
- A workload SHOULD obtain its credentials from the platform's identity service, rather than from a stored secret.
- A service that no external client needs to reach MUST be unreachable from the Internet.
- Servers SHOULD be immutable, with no interactive access.

## Cost

- Every estate MUST have a budget, with alerts on both actual and forecast spend.
- A service that is billed before any limit of ours can apply (e.g., inbound traffic at a proxy, or DNS lookups) MUST be unmetered.
