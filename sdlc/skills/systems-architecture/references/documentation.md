# Documenting a system's architecture

An architecture is documented so that another architect can assess it. What the design costs other stakeholders (e.g., a residual risk, or a limitation with no workaround) MUST be called out in the documents below.

## The architecture document

**The architecture document is the system's _constitution_**: the considerations, desiderata, and trade-offs that its design answers to, written up front to guide every later decision and change. A system designed from scratch MUST have one before it's built, and any other system SHOULD have one. Every change MUST comply with it. It SHOULD rarely be amended, and each amendment MUST be justified on its own merits, never by the change that prompted it.

The document MUST cover:

- The problem, stated separately from the design, so that either can be falsified without the other.
- The groups of users (e.g., staff and external users), followed by the other stakeholders (e.g., operators).
- The non-goals, and the deferred decisions.
- The leading alternative for each group of users and, where it serves a group better, what the system offers them instead.
- The most constrained environment the system must run in, and the users or other stakeholders that each constraint comes from (e.g., external users on a five-year-old Android version, or operators who must deploy on-premises).
- The components, which groups of users interact with each, what each knows about the people it serves (including what a broker can observe about the traffic it relays), and whom each trusts with what.
- Every party that stakeholders must trust, and with what. Where anonymity or deniability is a requirement, what each operator could be compelled to disclose, alter, or block, and the size of any crowd that anonymity depends on.
- Each backing service, named by the capability it provides (e.g., "an S3-compatible object store") rather than by product, wherever someone else could deploy the system. Where the system is coupled to one provider, it MUST say so, along with the layers that are deliberately not portable.
- The limit, caveat, or dependency that each delegation (to a provider, the platform, or third-party software) imposes.
- Each legal or contractual obligation that the design relies on, and what happens if it's breached.
- Each existing standard that could serve part of the design, whether it's adopted, and why.
- The threat model: the adversaries and their capabilities, including any capability that the design pre-empts and how far ahead that bet is. Each attack vector MUST state its impact, attempt likelihood, method, mitigations, and residual risks, and vectors SHOULD be ordered by likelihood. It MUST also say who bears each residual risk, and which mitigations fall to whoever deploys the system.
- Known limitations, including where there's no workaround.
- Each ethical cost that the design can't discharge.

## The change spec

A change spec specifies a change to the design before it's built, starting with the system's initial design, which introduces every element at once. It MUST use the medium that suits the change (e.g., an issue, a pull request, or an RFC). When writing one, `assets/change-spec.md` SHOULD be used as a guide, rather than as a strict template. When reviewing one, it MUST be judged on whether it provides what's needed to assess the change, whatever its structure.

- The spec MUST cover every element that the change introduces or alters in enough detail to be built and reviewed without guesswork. For example:
  - For each exchange: whether it's asynchronous, synchronous, or a stream (and, if synchronous, why it can't be asynchronous), the protocol, the message schema, authentication, size limits, timeouts, the retry policy (backoff, jitter, and whether it's capped by attempts or by time), and what happens once retries are exhausted.
  - For each endpoint that accepts traffic: rate limits, quotas, and other protections against abuse.
  - For each store: the schema, indices, uniqueness constraints, retention and what enforces it, and who can read it.
  - For each component: its identity and permissions, and how it's deployed and scaled.
  - For each failure mode: whose fault it is, the response, and the severity.
  - For each dependency: how the system behaves when it's unavailable.
  - For each configuration option: its default.
- Decisions nest, and each MUST state what it optimises for, at the expense of what, and its second-order consequences.
- Open questions MUST sit next to the decision they block.
- A rejected option MUST be kept, with its reasoning, rather than deleted.
- Where the author prefers an option for reasons they can't justify technically, the spec MUST say so, and MUST NOT turn that preference into a requirement (e.g., "I advise against alternative DNS roots, but I see no technical reason to ban them").
- Where the change drops a requirement or reverses a decision, the spec MUST:
  1. Restate the current design in its own best terms.
  2. Say what was wrong with the original requirement, on its own terms.
  3. Enumerate every simplification that the reversal buys.
  4. Enumerate the capabilities it costs and the consequences being accepted, and say why the advantages still outweigh them.
- The spec MUST be closed with the argument that settled it, including where the argument is that nothing was found to justify a change.
