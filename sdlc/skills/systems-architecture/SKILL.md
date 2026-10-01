---
name: systems-architecture
description: How to design systems beyond the process boundary. Scope, decomposition, data, messaging, failure, backing services, security and privacy, impact on others, operability, and tests. Use when designing, changing, or reviewing a system's architecture or its infrastructure code.
---
# Systems architecture

## Problem and scope

- The problem MUST be analysed independently of any solution to it (e.g., by surveying known approaches and their weaknesses) before a design is chosen.
- Before a mechanism is designed for a requirement, the requirement MUST be challenged: dropping one can remove a cascade of mechanisms (e.g., dropping peer authentication can remove a handshake, and a bespoke protocol). Every capability that the drop costs MUST be weighed against every simplification it buys.
- Where time or resources fall short, the problem MUST be narrowed (e.g., fewer use cases, platforms, or features), and the standard to which the rest is built MUST NOT be lowered.
- Non-goals MUST be decided before the design, and a mechanism that only serves a non-goal MUST NOT be built.
- Where an established standard does the job (e.g., a protocol, a data format, or a cryptographic scheme), it SHOULD be adopted in place of a bespoke mechanism. It SHOULD be declined only where it lacks a production-ready implementation in a language or on a platform that the system must support.
- The design MUST be compared against the leading alternative for each group of users it targets. Where the alternative serves a group better, the design MUST close the gap, or concede that group and decide what it offers them instead.
- The design MUST work in the most constrained environment it must support (e.g., hardware, connectivity, power, budget, or a platform that can't be upgraded), and treat anything better as an optimisation.
- Where a problem can't be solved by technical means alone, or a technical solution would be much simpler alongside a legal or contractual obligation (e.g., a no-logs clause for third-party operators), the design SHOULD rely on such an obligation, and MUST limit the damage should it be breached.
- Only what is expensive to reverse (e.g., identifiers, wire formats, and schemas) MUST be decided up front. The rest SHOULD wait for evidence.

## Decomposition

- Components MUST be delineated by coupling and cohesion first, and then given the least data, authority, and reach that their job requires.
- Two parts of the system MUST be separate components where different organisations operate them, or where they must start, stop, or scale independently (e.g., video transcoding that needs many more servers than the website that takes the uploads). They MUST also be separate where one must not hold data or authority that the other has. Otherwise, they SHOULD be one component.
- A component that some deployments don't need MUST be independently deployable.

## Data

- Data the system doesn't need MUST be designed out, rather than collected and protected by a promise not to look at it. This includes data about people who aren't users (e.g., the contacts in an uploaded address book).
- Every piece of data that is stored MUST have a purpose, a set of readers, and a retention period, and the store MUST enforce the retention period (e.g., with a TTL index).
- Personal data MUST NOT be replicated to a system with weaker retention, access control, or jurisdiction than its source.
- Idempotency MUST come from natural keys and a uniqueness constraint, rather than a record of what was done.

## Messaging

- Asynchronous messaging MUST be the default, because a message that is durably stored can be retried, redelivered, or dead-lettered after any failure, whereas request-response ties each component's availability to the others'. Request-response MUST be used only where the exchange can't be made asynchronous (e.g., a third-party API that only offers it).
- Every exchange MUST survive the other party being unreachable.
- Every message, whether exchanged synchronously or asynchronously, MUST carry the version of its format from its first release, because a version can't be retrofitted once messages are in use. The version MAY travel as metadata rather than in the payload (e.g., in the media type, such as `application/vnd.example.order.v1+json`, or in the event type).
- Work that many parties start at once (e.g., on a schedule, or in response to the same event) MUST be spread with random jitter, so that they don't act in lockstep.

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
- The threat model MUST include the system's own users and operators as adversaries of other users (e.g., a stalker abusing location sharing).
- A mitigation MUST NOT be assumed complete: for each, the design MUST identify what would defeat it, and whether those who bear that residual risk can accept it.
- Every entry point reachable by untrusted parties MUST be rate-limited.
- Where cost scales with something an attacker controls, the design MUST bound it.

## Impact beyond the system

- The system MUST NOT be able to overwhelm another system, whether ours or anyone else's, through abuse, a bug, or a misconfiguration, including at the scale the design targets. Every outbound flow MUST be capped per destination, and an input MUST NOT be able to trigger more outbound work than its sender could have done directly (e.g., through a webhook, a link preview, or a fan-out that turns one request into many).
- The system's environmental cost MUST be factored in: where providers or regions are otherwise comparable, the one powered by cleaner energy SHOULD be chosen, and work that can be deferred (e.g., batch jobs) SHOULD run where and when energy is cleanest.
- Resources the system consumes on devices it doesn't own (e.g., mobile data, battery, and storage) are a cost to their owners, and MUST NOT be spent on work that doesn't serve them unless they consent to it (e.g., relaying other users' traffic).
- Users MUST be able to leave with their data, in a documented format that another implementation could import.
- What runs on a user's device MUST keep doing whatever doesn't inherently need our servers when they're unreachable, including after the service shuts down.

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
