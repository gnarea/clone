---
name: systems-architecture
description: How to design systems beyond the process boundary. Scope, decomposition, data, messaging, failure, backing services, security and privacy, operability, and tests. Use when designing, changing, or reviewing a system's architecture or its infrastructure code.
---
# Systems architecture

## Problem and scope

- Before a mechanism is designed for a requirement, the requirement MUST be challenged: dropping one can remove a cascade of mechanisms (e.g., dropping peer authentication can remove a handshake, the certificates it needs, and a bespoke protocol). Every capability that the drop costs MUST be weighed against every simplification it buys.
- Where time or resources fall short, the problem MUST be narrowed (e.g., fewer use cases, platforms, or features), and the standard to which the rest is built MUST NOT be lowered.
- The problem MUST be analysed independently of any solution to it (e.g., by surveying known approaches and their weaknesses) before a design is chosen.
- Non-goals MUST be decided before the design, and a mechanism that only serves a non-goal MUST NOT be built.
- The design MUST be compared against the leading alternative for each group of users it targets. Where the alternative serves a group better, the design MUST close the gap, or concede that group and decide what it offers them instead.
- The design MUST work in the most constrained environment it must support (e.g., hardware, connectivity, power, budget, or a platform that can't be upgraded), and treat anything better as an optimisation.
- Where a problem can't be solved by technical means alone, or a technical solution would be much simpler alongside a legal or contractual obligation (e.g., a no-logs clause for third-party operators), the design SHOULD rely on such an obligation, and MUST limit the damage should it be breached.
- The design MUST weigh its consequences for every stakeholder, including those who never chose to be one, the collateral damage of its success, and its environmental cost. Where it imposes a cost it can't avoid, it MUST offset what it can for those who bear it.
- Only what is expensive to reverse (e.g., identifiers, wire formats, and schemas) MUST be decided up front. The rest SHOULD wait for evidence.

## Decomposition

- Components MUST be delineated by coupling and cohesion first, and then given the least data, authority, and reach that their job requires.
- A component that some deployments don't need MUST be independently deployable.

## Data

- Data the system doesn't need MUST be designed out, rather than collected and protected by a promise not to look at it.
- Every piece of data that is stored MUST have a purpose, a set of readers, and a retention period, and the store MUST enforce the retention period (e.g., with a TTL index).
- Personal data MUST NOT be replicated to a system with weaker retention, access control, or jurisdiction than its source.
- Idempotency MUST come from natural keys and a uniqueness constraint, rather than a record of what was done.

## Messaging

- Asynchronous messaging MUST be the default, because a message that is durably stored can be retried, redelivered, or dead-lettered after any failure, whereas request-response ties each component's availability to the others'. Request-response MUST be used only where the exchange can't be made asynchronous (e.g., a third-party API that only offers it).
- Every exchange MUST survive the other party being unreachable.
- Every message, whether exchanged synchronously or asynchronously, MUST carry the version of its format from its first release, because a version can't be retrofitted once messages are in use. The version MAY travel as metadata rather than in the payload (e.g., in the media type, such as `application/vnd.example.order.v1+json`, or in the event type).
- Work that many parties start at once (e.g., on a schedule, or in response to the same event) MUST be spread with random jitter, so that they don't act in lockstep.
- An established standard SHOULD be adopted where one fits, and SHOULD be declined only where no production-ready implementation exists for a platform the system must support.

## Failure

- The design MUST decide how the system behaves when each dependency is unavailable, and degraded operation MUST be a modelled state, not an error.
- Each failure mode MUST be attributed to the sender, the system, or the infrastructure, and the attribution MUST determine the response, the severity, and whether to retry. A failure that a later attempt can't overcome (e.g., malformed input) MUST NOT be retried.
- Every retry policy MUST be capped, by attempts or by elapsed time, and MUST space attempts with exponential backoff and jitter.
- A design whose failure path can't be made reliable MUST be rejected: where two stores would be updated together, a partial failure MUST be safe to repeat, unless the platform makes the write atomic.

## Backing services and providers

- The system MUST run as little as it can: managed services SHOULD be preferred, and compute SHOULD cost nothing whilst idle unless a requirement rules that out.
- Every delegation (to a provider, the platform, or third-party software) MUST be weighed against the limit, caveat, or dependency it imposes.
- Where others would deploy the system themselves, each backing service MUST be chosen by the capability it provides (e.g., an S3-compatible object store), behind an adapter that exposes only the operations that every supported backend offers in the same way.
- Where only we deploy the system, it SHOULD be coupled to a single provider.
- An abstraction whose upkeep outweighs the portability it buys (e.g., a pluggable database) MUST be refused.

## Security and privacy

### Trust

- Traffic that a component relays without needing to read MUST be encrypted end to end past it, and the metadata it observes MUST be minimised.
- The parties that stakeholders must trust, and what they must trust them with, MUST be minimised. Where trust can't be designed out, compliance MUST be verifiable from outside (e.g., by publishing the infrastructure code).
- Unsafe use of an API, a wire format, or a deployment's configuration MUST be impossible: no skipping a check, turning off a security property, or downgrading. Where a choice is unavoidable, offer a few named options, all of them safe.

### Anonymity

Where anonymity or deniability is a requirement:

- A single component MUST NOT hold enough to defeat it (e.g., both an address and the traffic sent to it).
- Operators SHOULD hold nothing that they could be compelled to disclose, alter, or block.
- Where anonymity depends on a crowd, the design MUST favour deployments that keep it large (e.g., a shared gateway over a self-hosted one).

### Threat model

- Every system MUST be designed against a threat model naming its adversaries and their capabilities, including those that are feasible today but not yet in use.
- A mitigation MUST NOT be assumed complete: for each, the design MUST identify what would defeat it, and whether those who bear that residual risk can accept it.
- Every entry point reachable by untrusted parties MUST be rate-limited.
- Where cost scales with something an attacker controls, the design MUST bound it.

## Operability

- An operator MUST be able to tell what the system is doing, how well, and whose fault a failure is, without a developer. Every behaviour observable from outside MUST be visible in logs, metrics, or traces.
- Severity MUST be set by who has to act, and how soon.
- Where privacy is a requirement, observability MUST be derived from the threat model: record what's needed to detect and troubleshoot abuse, and nothing that could identify a user.
- Deployment-time options SHOULD be kept to a minimum, and each default MUST be safe for every deployment.

## Tests

- Tests SHOULD use a real instance of every backing service, run locally or provisioned per test run. Where no such instance can be run (e.g., a proprietary service without an emulator), a test double MAY be used instead.
- Where tests use a substitute for the provider that a real deployment uses (e.g., an emulator, or a compatible alternative), the real provider MUST also be exercised on a schedule (e.g., weekly), rather than on every change, to catch drift and breaking changes.
- The deployed system SHOULD be testable end to end, through a supported artefact where third parties integrate with it.
- Tests MUST cover the most constrained environment that the design supports.

## Additional guidelines

Read a reference below where its condition holds; its rules apply in addition to the ones above.

### By artefact

- `references/server-side-systems.md`: The system runs on infrastructure that we or an operator run, and is reached over a network.
- `references/end-user-systems.md`: The system includes software installed on a device the user controls.

### By concern

- `references/asynchronous-messaging.md`: The design involves a broker, a queue, or any other exchange where the sender doesn't wait for the outcome.
- `references/synchronous-messaging.md`: The design involves request-response, whether as the client or the server.
- `references/contracts.md`: The change defines or alters a contract that another codebase, team, or organisation depends on.
- `references/cloud-infrastructure.md`: The change provisions or alters infrastructure at a cloud provider.
- `references/documentation.md`: The design, or a change to it, is being documented or proposed.
- `references/prototyping.md`: The artefact is a prototype built to answer a design question.
