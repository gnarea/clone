---
name: protocol-design
description: How to design protocols, as an extension of systems architecture. Scope, transports, failures, interoperability, wire formats, limits, identifiers, versioning and extensibility, intermediaries, and privacy. Use when designing, changing, or reviewing a protocol, a wire format, or a protocol specification.
---
# Protocol design

A _protocol_ is the messages that two or more parties exchange, their formats, and the rules for exchanging them, whether the parties are our own components or implementations that others build. This skill extends the /sdlc:systems-architecture skill, which applies in full, and only covers what changes when the design is a protocol.

## Scope

- The protocol MUST only prescribe the interactions that need its parties to agree. Whatever happens amongst the parties that a single operator controls (e.g., between a service's own applications) MUST be left to that operator.
- Every concern that the protocol leaves out (e.g., how an implementation stores messages, how applications handle each other's errors) MUST be assigned elsewhere (e.g., to the implementations, the applications, another protocol), and the specification MUST say where.
- Where other protocols are meant to be built on this one (e.g., a service that uses it to authenticate its users), they MAY narrow what it allows (e.g., a lower limit, fewer algorithms), but MUST NOT widen it. The specification MUST say what each of them has to define.

## Transports

- Every mechanism, including authentication and key agreement, MUST work with the delay, loss, duplication, and reordering of the transports that carry it.

Where the protocol is expected to run over more than one transport (e.g., HTTP, a message broker, removable media):

- Its core MUST be specified independently of any transport, and each transport MUST be specified separately as a _binding_.
- A binding MAY extend the core, but MUST NOT override it. A requirement that more than one binding would need belongs in the core, and one that a single binding needs belongs in that binding.
- A binding SHOULD carry the core's messages as opaque bytes, so that the format native to its transport (e.g., Protocol Buffers in gRPC) never carries the protocol's semantics.
- A new transport MUST be supported through a new binding, rather than a change to the core.

## Failures

- Where a failure is the sender's fault (e.g., an invalid message), the recipient SHOULD tell it what was wrong, unless there's a reason not to (e.g., the answer would enable an enumeration attack).
- Where there is such a reason, the refusal MUST look the same as the outcomes that reveal nothing.
- The protocol, or each of its bindings where it has them, MUST say how implementations treat a signal that it doesn't define (e.g., an undocumented HTTP status code).

## Interoperability

- Every option that the protocol offers, including those that a standard it adopts leaves open, is a way for two conforming implementations to fail to interoperate. Each MUST be justified, and where one choice serves every use case, the protocol MUST mandate it.
- Where a mandatory-to-implement choice will do, a parameter (e.g., a version, an algorithm, a binding) MUST NOT be negotiated. It MUST be mandated by the protocol, declared by the sender in the message, or published by the recipient in advance (e.g., in a DNS record), and the recipient MUST refuse what it doesn't support.
- A requirement MUST NOT be added unless what it relies on (e.g., an algorithm) has a production-ready implementation on every platform that the protocol must support, and those implementations interoperate with each other. Where a platform lacks one, the protocol MAY degrade gracefully on that platform, as an alternative to dropping the platform.
- A requirement that proves hard to implement with the mainstream tools of a supported platform SHOULD be reconsidered.
- Each party MUST be strict about what it sends, and MUST only verify what's relevant to it in what it receives (aka the _robustness principle_).
- Every constraint that the protocol places on one party MUST be enforced by the parties that rely on it (e.g., a verifier refusing a credential that outlasts the maximum validity period), so that a lax party can't reintroduce the risk that the constraint guards against.
- Where services are built on the protocol, it SHOULD define a trivial one of its own (e.g., a ping), so that implementations and deployments can be tested end-to-end.

## Wire formats

- Messages SHOULD be serialised in a binary format (e.g., ASN.1 DER, Protocol Buffers), for performance.
- The type of a message and the version of its format MUST always travel with it. They SHOULD travel as metadata where the transport carries it reliably (e.g., a media type), and in the payload otherwise.

## Limits

- Every limit MUST be an exact number (e.g., in octets, in seconds). Where it's derived from other limits, the specification MUST show the arithmetic (e.g., the largest payload plus the overhead of the fields around it), and where it's arbitrary, the specification MUST say so.
- Where messages carry an expiry date, the protocol MUST cap how far ahead it can be.
- Where parties exchange timestamps, the tolerance for clock skew SHOULD depend on how well the parties involved can keep time (e.g., hours where one of them can be offline for weeks), rather than be a single figure for the whole protocol.

## Identifiers

- The specification MUST NOT require implementations to interpret an identifier that they only need to compare (e.g., a certificate serial number), so that they can treat it as an opaque value.
- A party's identifier SHOULD be derived from its key (e.g., a digest of the public key), unless people have to read it.
- Where a party is identified by a name that people read (e.g., a user name), the protocol MUST constrain the name to make it harder to pass one off as another (e.g., a PRECIS profile, a ban on the character that separates a name from its domain).

## Versioning and extensibility

- Each format and interface MUST carry its own version, in the identifier native to it (e.g., an octet in a binary format, a field in a schema, a segment in a URL path, a media type), so that each can evolve independently. An incompatible change MUST get a new identifier, whilst a compatible one MAY keep the existing one.
- An upgrade MUST NOT require every party to upgrade at once: during the transition, recipients MUST accept the previous version alongside the new one. A message whose type or version a recipient doesn't recognise MUST be refused, and MUST NOT cause any other failure.
- Every identifier that could clash with one that someone else assigns (e.g., a message type, an algorithm identifier) MUST be allocated from a namespace that the protocol's owner controls (e.g., an OID arc, the vendor tree of media types), and MUST NOT be reassigned. Third parties that extend the protocol MUST allocate theirs outside that namespace.
- Where a value may need to be added or withdrawn without a new version of the protocol (e.g., an algorithm), the values MUST be listed in a registry that can change independently of the protocol, including to deprecate one.
- A value MAY be reserved for an addition that's foreseeable but not yet feasible (e.g., a key type that some supported platforms lack), so that it can arrive without a change to the format.

## Intermediaries

- Where messages pass through an intermediary (e.g., a broker), the protocol SHOULD provide a way to detect or avoid the messages that it drops.
- Every party that handles a message, including one that only relays it, MUST validate what's relevant to it before processing or relaying the message.

## Privacy

Where privacy is a requirement:

- The protocol MUST be assessed for what each party that handles or observes a message learns from it besides its content (e.g., when it was created, its size, who initiated the exchange, what the recipient asked for). Each leak MUST be mitigated in the protocol itself (e.g., by backdating a timestamp, padding the message, moving a field inside the encrypted payload), or the specification MUST state what the party learns.
- Every identifier and credential that a message exposes MUST be assessed for whether it lets an observer link one party's activity across its peers (e.g., the same intermediate certificate in every message), and SHOULD be left out where it does.
- Privacy requirements on the services that the protocol relies on (e.g., encrypted DNS resolution) MUST be part of the protocol, rather than left to deployment guidance.
- A countermeasure to traffic analysis MUST be assessed for whether it makes the traffic stand out (e.g., a pattern that changes with every connection, a pattern that every endpoint shares), and against an adversary who controls the component that applies it (e.g., a compromised relay that hands out decoy traffic to see who collects it).

## Additional guidelines

### By concern

- [Cryptographic protocols](references/cryptographic-protocols.md): The protocol signs, encrypts, or authenticates messages, or issues credentials.
- [Delay-tolerant networking](references/delay-tolerant-networking.md): Messages can take days to arrive, or pass through intermediaries that store them and forward them later.
- [Specifications](references/specifications.md): The protocol is being specified, or its specification changed.
