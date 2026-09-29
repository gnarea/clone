---
name: systems-architecture
description: How to design systems beyond the process boundary. Decomposition, data, threats, failure, cost, operability, and backing services. Use when designing, changing, or reviewing a system's architecture or its infrastructure code.
---
# Systems architecture

The sections below follow the order of the priorities they serve, so where two rules conflict, the earlier one wins.

## Security and privacy

### Decomposition

- Components MUST be delineated by coupling and cohesion first, so that what changes together lives together. Each component MUST then be given the least data, authority, and reach that its job requires.
- The design MUST state what each component knows about the people it serves, and where a component exists only to broker between two others, what it may observe about the traffic it brokers.
- Where anonymity or deniability is a requirement:
  - A single component MUST NOT hold enough to defeat it. Two pieces of data that identify someone by being held together (e.g., an address and the traffic sent to it) MUST be split across components under separate control, or one of them dropped.
  - The design MUST state what each component's operator could be compelled to disclose, alter, or block, and MUST prefer a design in which the answer is "nothing".
  - Where anonymity depends on a crowd, the design MUST state how large that crowd is, and MUST warn against deployments that shrink it (e.g., a single-user instance).

### Data

- Data that the system doesn't need MUST be designed out, rather than collected and then protected by a promise not to look at it.
- Every component that stores anything MUST document what it stores, why, who can see it, and for how long, even where the answer is "nothing".
- Personal data MUST NOT be replicated to a system whose retention, access control, or jurisdiction is weaker than that of the system it came from.

### Trust

- The design MUST name every party that stakeholders are required to trust, and what each is trusted with, and MUST minimise both.
- Where trust can't be designed out, compliance MUST be verifiable from outside, rather than rest on an operator's word.
- The unsafe use of an API, a wire format, or a deployment's configuration MUST be impossible, rather than merely discouraged. There MUST be no way to skip a check, turn off a security property, or downgrade to a weaker option. Where a choice is unavoidable, the design MUST offer a few named options, all of them safe.

### Threats

- Every system MUST have a threat model that names its adversaries and their capabilities.
- Each attack vector MUST state its impact, how likely it is to be attempted, the attack method, the mitigations, and the residual risks. Vectors SHOULD be ordered by attempt likelihood.
- A vector MUST NOT have an empty residual risk. Where a mitigation is believed to be complete, the entry MUST say what would defeat it.
- Residual risks MUST be stated where the people who bear them will see them.
- Where the design pre-empts a capability that the adversary doesn't have yet, it MUST name that capability and how far ahead the bet is, so that the bet can be revisited.

## Ethics

- The design MUST weigh its consequences for every stakeholder, including those who never chose to be one, and MUST account for the collateral damage the system would cause by succeeding.
- The environmental cost of running the system MUST be estimated, and weighed like any other cost.
- An ethical cost that the design can't discharge MUST be recorded against the design as such, and MUST NOT be presented as anything else.

## Fitness for purpose

### Scope

- A requirement MUST be challenged before a mechanism is designed to satisfy it. Where dropping one is proposed, the proposal MUST enumerate every simplification it buys and every capability it costs.
- Where quality can't be afforded, the scope MUST be narrowed until what remains can be built without compromising on quality.
- The problem MUST be stated separately from the design, so that either can be falsified without the other.
- The non-goals MUST be stated at the start of the design, and repeated wherever adoption is decided.
- Where a leading alternative serves some users better, the design MUST say so, name those users, and describe what the system offers them instead.
- Only what is expensive to reverse later (e.g., identifiers, wire formats, and data schemas) MUST be decided up front. Everything else SHOULD be deferred until evidence arrives.

### Constraints

- The design MUST name the most constrained environment the system must run in, whether the constraint is hardware, connectivity, power, budget, or a platform that can't be upgraded, and MUST work there. Anything better MUST be treated as an optimisation.
- Where policy (e.g., a legal or contractual requirement) makes a technical problem simpler or solves it outright, the design MUST say so, and MUST state what happens where the policy is breached.

## Resilience

### Communication

- Every exchange MUST be designed to survive the other party being unreachable. Messages that can be stored and retried SHOULD be preferred to request-response, which ties each component's availability to that of the others.
- The design MUST state what the system does when each of its dependencies is unavailable, and degraded operation MUST be a modelled state rather than an error.

### Failure

- For each failure mode, the design MUST attribute the fault to the sender, to the system itself, or to the infrastructure, and that attribution MUST determine the response returned, the severity logged, and whether the work is retried or dropped. Only what a later attempt could survive MUST be retried.
- Retries and dead-lettering MUST be left to the broker or platform, configured by the operator. The application MUST only report whether a later attempt could succeed.
- An acknowledgement MUST be sent only once the work is safe for the sender to forget: durably stored and flushed (e.g., `fdatasync`, or `FlushFileBuffers`), not merely received or parsed.
- A design whose failure path can't be made reliable MUST be rejected. Where two stores would have to be updated together, the design MUST be changed so that a partial failure is safe to repeat, unless the platform makes the write atomic.
- Idempotency MUST be achieved with natural keys and a uniqueness constraint, rather than with a record of what has already been done.

## Cost

- The system MUST run as little as it can. A managed service SHOULD be preferred to one that we would operate, and compute SHOULD cost nothing whilst idle. Anything that must stand idle MUST be justified by a requirement that scaling to zero would break.
- Every delegation to a provider, to the platform, or to third-party software MUST state the limit, caveat, or dependency that it imposes.
- Where the cost scales with something that an attacker controls, the design MUST bound it and state the bound.

## Operability

- An operator MUST be able to tell what the system is doing, how well, and whose fault it is when something goes wrong, without a developer to hand. Every behaviour observable from outside MUST be visible in logs, metrics, or traces.
- The severity of every signal MUST be set by who has to act, and how soon.
- Where privacy is a requirement, the observability policy MUST be derived from the threat model: whatever an operator needs in order to detect and troubleshoot abuse MUST be recorded, and anything that could identify a user MUST NOT be.
- Every deployment-time choice MUST be documented, and a component SHOULD run with no configuration at all where its defaults can serve every deployment.
- A component that some deployments don't need MUST be deployable independently, and the documentation MUST say which deployments those are.

## Replaceability

- An abstraction over interchangeable providers MUST be justified by who would otherwise have to reimplement the system. Where the answer is nobody outside the team, the design SHOULD couple to one provider, and MUST say so.
- Where an abstraction is warranted, the design MUST state which layers are portable and which are deliberately not, and MUST refuse an abstraction whose upkeep costs more than the portability it buys.
- Documentation MUST name capabilities rather than implementations (e.g., "an S3-compatible object store"), so that an operator reads what they must supply, rather than what we run.
- An established standard SHOULD be adopted where one covers the problem, and declining it MUST be recorded with the reason.
- A contract that another system depends on MUST be versioned from its first release, MUST evolve by addition, and MUST NOT be broken for anything less than a correctness or security fix.

## Testing the system

- Every backing service MUST be runnable locally, or have a real equivalent that tests can provision per run. A component that can only be exercised against production is a design defect, and MUST be redesigned rather than mocked.
- The provider that a real deployment would use MUST be exercised by automated tests.
- The design SHOULD include a way of exercising the deployed system end to end. Where third parties integrate with it, that SHOULD be a supported artefact rather than a test fixture.
- Tests MUST cover the most constrained environment named by the design.

## Design records

- Every architectural decision MUST be proposed and argued in the issue tracker before it is implemented, using the template in `references/design-records.md`.
- Each decision MUST state what it optimises for and at the expense of what, following it through to its second-order consequences.
- Open questions MUST be published next to the decision they block, rather than tracked out of sight.
- A rejected option MUST keep its reasoning, marked as rejected, rather than be deleted.
- Where the author has a stake in the outcome, or a preference they can't fully justify, they MUST flag it in the document itself.

## Additional guidelines

Read a reference below where its condition holds; its rules apply in addition to the ones above.

### By artefact

- `references/server-side-systems.md`: The system runs on infrastructure that we or an operator run, and is reached over a network.
- `references/end-user-systems.md`: The system includes software installed on a device the user controls.

### By concern

- `references/api-design.md`: The change defines or alters a contract that another codebase, team, or organisation depends on.
- `references/cloud-infrastructure.md`: The change provisions or alters infrastructure at a cloud provider.
- `references/design-records.md`: The change is being proposed, or the product's standing architecture document is being written or revised.
- `references/prototyping.md`: The artefact is a prototype or a proof of concept, built to answer a design question.
