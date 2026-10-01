# Documenting a system's architecture

## The architecture document

Each product MUST have a standing architecture document that every change is judged against, and a change MUST amend it rather than leave it for later. It MUST cover:

- The problem, stated separately from the design, so that either can be falsified without the other.
- The non-goals, and the deferred decisions.
- The most constrained environment the system must run in.
- The components, what each knows about the people it serves (including what a broker can observe about the traffic it relays), and whom each trusts with what.
- Every party that stakeholders must trust, and with what. Where anonymity or deniability is a requirement, what each operator could be compelled to disclose, alter, or block, and the size of any crowd that anonymity depends on.
- The contracts between components, and with the systems they depend on or serve.
- What each component stores, why, who can see it, and for how long, even where the answer is "nothing".
- How the system behaves when each dependency is unavailable.
- Each backing service, named by the capability it provides (e.g., "an S3-compatible object store") rather than by product, wherever someone else could deploy the system. Where the system is coupled to one provider, it MUST say so, along with the layers that are deliberately not portable.
- The limit, caveat, or dependency that each delegation (to a provider, the platform, or third-party software) imposes.
- Each legal or contractual obligation that the design relies on, and what happens if it's breached.
- Every deployment configuration option, and its default.
- Each standard that was declined where one fitted, and why.
- The threat model: the adversaries and their capabilities, including any capability that the design pre-empts and how far ahead that bet is. Each attack vector MUST state its impact, attempt likelihood, method, mitigations, and residual risks, and vectors SHOULD be ordered by likelihood.
- Each ethical cost that the design can't discharge.

## Proposing a design or a change

A proposal MUST use the medium that suits the change (e.g., an issue, a pull request, or an RFC), structured per `assets/design-proposal.md`.

- The proposed design MUST specify every element it introduces or changes in enough detail to be built and reviewed without guesswork. For example:
  - For each exchange: whether it's synchronous or asynchronous (and, if synchronous, why it can't be asynchronous), the protocol, the message schema, authentication, size limits, timeouts, the retry policy (backoff, jitter, and whether it's capped by attempts or by time), and what happens once retries are exhausted.
  - For each endpoint that accepts traffic: rate limits, quotas, and other protections against abuse.
  - For each store: the schema, indices, uniqueness constraints, retention and what enforces it, and who can read it.
  - For each component: its identity and permissions, and how it's deployed and scaled.
  - For each failure mode: whose fault it is, the response, and the severity.
- Decisions nest, and each MUST state what it optimises for, at the expense of what, and its second-order consequences.
- Open questions MUST sit next to the decision they block.
- A rejected option MUST be kept, with its reasoning, rather than deleted.
- Where the author prefers an option for reasons they can't justify technically, the proposal MUST say so, and MUST NOT turn that preference into a requirement (e.g., "I advise against alternative DNS roots, but I see no technical reason to ban them").

## Arguing for a reversal

Where a proposal drops a requirement or reverses a decision, it MUST:

1. Restate the current design in its own best terms.
2. Say what was wrong with the original requirement, on its own terms.
3. Enumerate every simplification that the reversal buys.
4. Enumerate the capabilities it costs and the consequences being accepted, and say why the advantages still outweigh them.

## Settling a decision

A proposal MUST be closed with the argument that settled it, including where the argument is that nothing was found to justify a change.

## Disclosure

What those affected by the design need in order to decide whether to adopt it MUST be published where they'll see it (e.g., the product's website or the operator documentation), not only in the architecture document:

- The non-goals.
- Where a leading alternative serves some users better, and what the system offers them instead.
- The residual risks, to those who bear them.
- Known limitations, in plain language, including where there's no workaround.
- Every deployment configuration option, to operators.
