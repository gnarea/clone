---
name: systems-architecture
description: How to design systems beyond the process boundary. Decomposition, data, threats, failure, cost, operability, and backing services. Use when designing, changing, or reviewing a system's architecture or its infrastructure code.
---
# Systems architecture

## Problem and scope

- A requirement MUST be challenged before a mechanism is designed for it. A proposal to drop one MUST enumerate every simplification it buys and every capability it costs.
- Where quality can't be afforded, the scope MUST be narrowed instead.
- The problem MUST be stated separately from the design, so that either can be falsified without the other.
- Non-goals MUST be stated at the start of the design, and wherever adoption is decided.
- Where a leading alternative serves some users better, the design MUST say so, and what it offers them instead.
- The design MUST name the most constrained environment it must work in (e.g., hardware, connectivity, power, budget, or a platform that can't be upgraded), and treat anything better as an optimisation.
- Where policy (e.g., a legal or contractual requirement) does technical work, the design MUST say so, and what happens if the policy is breached.
- The design MUST weigh its consequences for every stakeholder, including those who never chose to be one, the collateral damage of its success, and its environmental cost.
- An ethical cost the design can't discharge MUST be recorded as such.

## Decomposition

- Components MUST be delineated by coupling and cohesion first, and then given the least data, authority, and reach that their job requires.
- A component that some deployments don't need MUST be independently deployable.

## Data

- Data the system doesn't need MUST be designed out, rather than collected and protected by a promise not to look at it.
- Every component that stores anything MUST document what, why, who can see it, and for how long, even where the answer is "nothing".
- Personal data MUST NOT be replicated to a system with weaker retention, access control, or jurisdiction than its source.
- Idempotency MUST come from natural keys and a uniqueness constraint, rather than a record of what was done.

## Communication between components

- Every exchange MUST survive the other party being unreachable. Messages that can be stored and retried SHOULD be preferred to request-response.
- An acknowledgement MUST be sent only once the work is safe for the sender to forget: durably stored and flushed (e.g., `fdatasync`), not merely received or parsed.
- A design whose failure path can't be made reliable MUST be rejected: where two stores would be updated together, a partial failure MUST be safe to repeat, unless the platform makes the write atomic.
- An established standard SHOULD be adopted where one fits, and declining it MUST be recorded with the reason.

## Failure

- The design MUST state what happens when each dependency is unavailable, and degraded operation MUST be a modelled state, not an error.
- Each failure mode MUST be attributed to the sender, the system, or the infrastructure, and the attribution MUST determine the response, the severity, and whether to retry. Only what a later attempt could survive MUST be retried.
- Retries and dead-lettering MUST be left to the broker or platform. The application MUST only report whether a later attempt could succeed.

## Backing services and providers

- The system MUST run as little as it can: managed services SHOULD be preferred, and compute SHOULD cost nothing whilst idle unless a requirement rules that out.
- Every delegation (to a provider, the platform, or third-party software) MUST state the limit, caveat, or dependency it imposes.
- An abstraction over interchangeable providers MUST be justified by who would otherwise have to reimplement the system. Where nobody outside the team would, the design SHOULD couple to one provider, and MUST say so.
- Where an abstraction is warranted, the design MUST state which layers are deliberately not portable, and MUST refuse one whose upkeep outweighs the portability it buys.
- Documentation MUST name capabilities rather than implementations (e.g., "an S3-compatible object store").

## Security and privacy

### Trust

- The design MUST state what each component knows about the people it serves, including what a broker may observe about the traffic it relays.
- The design MUST name every party that stakeholders must trust, and with what, and MUST minimise both. Where trust can't be designed out, compliance MUST be verifiable from outside.
- Unsafe use of an API, a wire format, or a deployment's configuration MUST be impossible: no skipping a check, turning off a security property, or downgrading. Where a choice is unavoidable, offer a few named options, all of them safe.

### Anonymity

Where anonymity or deniability is a requirement:

- A single component MUST NOT hold enough to defeat it (e.g., both an address and the traffic sent to it).
- The design MUST state what each operator could be compelled to disclose, alter, or block, and SHOULD make the answer "nothing".
- Where anonymity depends on a crowd, the design MUST state its size, and warn against deployments that shrink it.

### Threat model

- Every system MUST have a threat model naming its adversaries and their capabilities.
- Each attack vector MUST state its impact, attempt likelihood, method, mitigations, and residual risks, and vectors SHOULD be ordered by likelihood.
- A vector MUST NOT have an empty residual risk: where a mitigation seems complete, say what would defeat it. Residual risks MUST be stated where those who bear them will see them.
- Where the design pre-empts a capability the adversary doesn't have yet, it MUST name it and how far ahead the bet is.
- Where cost scales with something an attacker controls, the design MUST bound it and state the bound.

## Operability

- An operator MUST be able to tell what the system is doing, how well, and whose fault a failure is, without a developer. Every behaviour observable from outside MUST be visible in logs, metrics, or traces.
- Severity MUST be set by who has to act, and how soon.
- Where privacy is a requirement, observability MUST be derived from the threat model: record what's needed to detect and troubleshoot abuse, and nothing that could identify a user.
- Every deployment-time choice MUST be documented, and defaults SHOULD serve every deployment.

## Testing the system

- Every backing service MUST be runnable locally, or have a real equivalent provisioned per test run. A component that can only be exercised in production MUST be redesigned rather than mocked.
- The provider a real deployment would use MUST be exercised by automated tests.
- The deployed system SHOULD be testable end to end, through a supported artefact where third parties integrate with it.
- Tests MUST cover the most constrained environment the design names.

## Design records

- Every architectural decision MUST be argued in the issue tracker before it's implemented, per `references/design-records.md`.
- Only what is expensive to reverse (e.g., identifiers, wire formats, and schemas) MUST be decided up front. The rest SHOULD wait for evidence.
- Each decision MUST state what it optimises for, at the expense of what, and its second-order consequences.
- Open questions MUST sit next to the decision they block.
- A rejected option MUST be kept, with its reasoning, rather than deleted.
- An author with a stake in the outcome, or a preference they can't justify, MUST say so in the document.

## Additional guidelines

Read a reference below where its condition holds; its rules apply in addition to the ones above.

### By artefact

- `references/server-side-systems.md`: The system runs on infrastructure that we or an operator run, and is reached over a network.
- `references/end-user-systems.md`: The system includes software installed on a device the user controls.

### By concern

- `references/contracts.md`: The change defines or alters a contract that another codebase, team, or organisation depends on.
- `references/cloud-infrastructure.md`: The change provisions or alters infrastructure at a cloud provider.
- `references/design-records.md`: The change is being proposed, or the product's architecture document is being written or revised.
- `references/prototyping.md`: The artefact is a prototype built to answer a design question.
