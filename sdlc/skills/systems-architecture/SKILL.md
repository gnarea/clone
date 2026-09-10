---
name: systems-architecture
description: How to design or review anything beyond the process boundary, and how to record those decisions. Trust boundaries, data and retention, threats, failure paths, cost, deployment topology, and backing services. Use when designing, changing, or reviewing a system's architecture or its infrastructure code.
---
# Systems architecture

The subject of this skill is everything outside the application's OS process: what talks to what, over which contract, holding which data, running on whose infrastructure, and what happens when any of it fails.

## Decomposition

- Components MUST be delineated by what each is allowed to know, rather than by the work each performs. Where the two decompositions disagree, the trust boundary wins.
- Each component MUST be given the least data, authority, and reach that its job requires, and the design MUST state what each one knows about the people it serves.
- Where a single component would hold two pieces of data that identify someone by being held together (e.g., an address and the traffic sent to it), the design MUST split them across components under separate control, or drop one.
- For each component, the design MUST answer what its operator could be compelled to disclose, alter, or block, and MUST prefer a design in which the answer is "nothing".
- Where a component exists only to broker between two others, the design MUST state what it may observe about the traffic it brokers.

## Data and retention

- Every component that stores anything MUST document, under a standing heading, what it stores, why, and for how long. That heading MUST be answered even where the answer is "nothing".
- Retention MUST be enforced by the storage engine (e.g., a TTL index, or an object lifecycle policy), so that it holds whether or not the application is running or correct.
- An identifier MUST NOT be reusable to correlate a person across services, and where correlation is unavoidable, the component that can perform it MUST be named in the design.
- Where anonymity depends on a crowd, the design MUST state how large that crowd is, and MUST warn against deployments that shrink it (e.g., a single-user instance).
- Personal data MUST NOT be replicated to a system whose retention, access control, or jurisdiction is weaker than that of the system it came from.

## Threats

- Every system MUST have a threat model that names its adversaries and their capabilities, and it MUST be published with the design.
- Each attack vector MUST state its impact, how likely it is to be attempted, the attack method, the mitigations, and the residual risks. Vectors MUST be ordered by attempt likelihood.
- A vector MUST NOT have an empty residual risk. Where a mitigation is believed to be complete, the entry MUST say what would defeat it.
- The model MUST account for capabilities the adversary is expected to acquire within three to five years, not only those observed today.
- The design MUST assume that its own operators are targets, and MUST minimise what coercing them would yield.

## Transparency and assurance

- The design, the source code, and the infrastructure code MUST be public, so that a coerced or covert change is a public change. Security MUST NOT rest on the secrecy of a mechanism, including an obfuscation mechanism.
- The design MUST be independently assessed before it is implemented, and the system reassessed once deployed. Every report MUST be published in full, without rebuttal or quiet revision, along with a summary in our own words and whatever we have chosen not to act on.

## Scope

- The non-goals MUST be stated in the first section of the design, and repeated wherever adoption is decided, including customer-facing material.
- A requirement MUST be challenged before a mechanism is designed to satisfy it. Where dropping one is proposed, the proposal MUST enumerate every simplification it buys and every capability it costs.
- Where a leading alternative serves some users better, the design MUST say so, name those users, and describe what the system offers them instead.
- The problem MUST be stated in a document that proposes no solution, so that the problem statement and the design can be falsified independently.
- A design MUST NOT be scoped by dates. Deferred work MUST carry the criteria that would bring it forward, and the reason it isn't being done now.
- Work that is deferred but expensive to retrofit MUST be reserved: give it an identifier, a statement of intent, and its open questions, and leave the rest unspecified.

## Contracts between systems

- A seam that crosses a language, an organisation, or a trust boundary MUST be realised as a separate process speaking a wire format that anyone can implement, rather than as a library that only one stack can consume.
- A seam inside one language and one team SHOULD be realised as a library, and anything that is an implementation detail rather than a requirement of the contract MUST live there rather than in the contract.
- Where the implementation is delegated to others, the wire format, the cryptography, and the failure taxonomy MUST be confined to a platform-independent library of our own, written before the applications that consume it, so that the perimeter is a package rather than a convention about who writes which file.
- Security-critical code MUST be rewritten rather than reviewed into shape, and a security control that only appears to work MUST be treated as a defect rather than a missing feature.
- Delay MUST be the normal case rather than the exception: a design MUST still work when a reply arrives hours or days later, or never.
- Asynchronous messaging SHOULD NOT be used to emulate request-response.

## Failure

- For each failure mode, the design MUST attribute the fault to the sender, to us, or to the infrastructure, and that attribution MUST determine the response returned, the severity logged, and whether the work is retried or dropped. What is malformed, unauthorised, or expired MUST NOT be retried; only what a later attempt could survive MUST be.
- The application MUST NOT implement retries or failure notifications of its own. It MUST report whether a later attempt could succeed, and leave retries and dead-lettering to the broker or platform that the operator configures.
- An acknowledgement MUST be sent only once the work is safe for the sender to forget: durably stored and flushed (e.g., `fdatasync`, or `FlushFileBuffers`), not merely received or parsed.
- A design that requires two stores to be updated together MUST be rejected in favour of one where a partial failure is safe to repeat, unless the platform makes the write atomic.
- Idempotency MUST be achieved with natural keys and a uniqueness constraint, rather than with a record of what has already been done.
- The design MUST state what the system does when each of its dependencies is unavailable, and offline or degraded operation MUST be a modelled state rather than an error.

## Cost

- Compute SHOULD be serverless and scale to zero. Anything that must stand idle MUST be justified by a requirement that scaling to zero would break.
- A managed service SHOULD be preferred to one we would operate, unless its terms, its jurisdiction, or its support for the cryptography we need rules it out.
- Where a design's cost scales with something an attacker controls, the design SHOULD bound it, and MUST state the bound.
- Where money or policy is doing security work (e.g., a price that deters enumeration, or a contractual prohibition on logging), the design MUST say so, and MUST state the conflict this creates with the product's mission and what compensates for it.
- Obligations placed on third parties MUST be written as normative requirements, and any political or jurisdictional judgement they rest on MUST be delegated to a citable third-party index rather than asserted by us.

## Operability

- The system MUST be operable by someone who has no access to us. Every deployment-time choice MUST be documented, and a component SHOULD run with no configuration at all where its defaults can serve every deployment.
- Documentation MUST name capabilities rather than implementations (e.g., "an S3-compatible object store"), so that an operator reads what they must supply rather than what we run.
- Documentation MUST be split by audience, and each part MUST say who it is for: the repository documents what contributors and integrators need, and the product's documentation what operators and end users need.
- A component that some deployments don't need MUST be independently deployable, and the documentation MUST say which those are.
- Promotion to production MUST be a deliberate, separate act, distinct from merging or building.
- The observability policy MUST be derived from the threat model: whatever an operator needs in order to detect and troubleshoot abuse MUST be recorded, and anything that could identify a user MUST NOT be, whichever way a general convention would point.

## Backing services and platforms

- An abstraction over interchangeable providers MUST be justified by who would otherwise have to reimplement the system. Where the answer is nobody outside the team, coupling to one provider is the better trade, and MUST be stated plainly.
- Where an abstraction is warranted, the design MUST state which layers are portable and which are deliberately not, and MUST refuse an abstraction whose maintenance cost outweighs the portability it buys.
- The portable path MUST be the one under test: the provider that a real deployment would use MUST be exercised by automated tests, so that the path an operator depends on cannot rot.
- An established standard MUST be adopted where one covers the problem. Declining one is justified only by the readiness of implementations for every platform the system must support, and MUST be recorded with the preconditions that would reverse the decision.
- Where a dependency forces a compromise into the design, that compromise MUST be recorded against the design, indexed by the dependency that caused it, so that it can be revisited when the dependency changes.
- Work SHOULD be delegated to the platform, or to widely deployed third-party software, where the property needed is simplicity, robustness, performance, security, or the absence of a distinguishing fingerprint. Every such delegation MUST state the limit or caveat it imposes.
- A dependency MUST be dropped where its terms of service, its jurisdiction, or its incident history changes the risk the system carries.

## Testing the system

- Every backing service MUST be runnable locally, or have a real equivalent that tests can provision per run. A component that can only be exercised against production is a design defect, and MUST be redesigned rather than mocked.
- The design SHOULD include a way of exercising the deployed system end to end. Where third parties integrate with it, that way SHOULD be a supported artefact rather than a test fixture.
- Tests MUST cover the worst hardware, operating system version, and network conditions that a user plausibly has, and results MUST be reported per network or region wherever those differ materially.

## Design records

- Every architectural decision MUST be proposed and argued in the issue tracker before it is implemented, using the template in `references/design-records.md`.
- Open questions MUST be published inside the document the decision lives in, next to the decision they block, rather than tracked out of sight.
- A rejected or abandoned option MUST keep its identifier and its reasoning, marked as rejected, rather than be deleted.
- An issue MUST be closed with the argument that settled it, including where the argument is that nothing was found to justify a change.
- Where the author has a stake in the outcome, or a preference they can't fully justify, they MUST flag it in the document itself.
- A decision MUST graduate as it stabilises: from the issue thread, to the repository's documentation, to the product's documentation, and finally to a specification.
- The design SHOULD be published before its implementation exists, and reviewed as an artefact in its own right. Formalise early where others will implement against it, and late whilst we are still learning what the system is.

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
