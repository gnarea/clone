---
name: protocol-design
description: How to design protocols, as an extension of systems architecture. Scope, bindings, exchanges, failures, interoperability, wire formats, limits, identifiers, versioning and extensibility, delivery, and privacy. Use when designing, changing, or reviewing a protocol, a wire format, or a protocol specification.
---
# Protocol design

A _protocol_ is the messages that two or more parties exchange, their formats, and the rules for exchanging them, whether the parties are our own components or implementations that others build. This skill extends the /sdlc:systems-architecture skill, which applies in full, and only covers what changes when the design is a protocol.

## Scope

- Where the protocol spans more than one layer (e.g., an application, the broker that relays its messages, the network between brokers), it MUST prescribe only how each layer interacts with those adjacent to it, and leave what happens within a layer to whoever operates it.
- Every concern that the protocol leaves out (e.g., how an implementation stores messages, how applications handle each other's errors) MUST be assigned elsewhere (e.g., to the implementations, the applications, another protocol), and the specification MUST say where.

## Bindings

Where the protocol may need to run over more than one transport (e.g., HTTP, a message broker, removable media):

- Its core MUST be specified independently of any transport, and each transport MUST be specified separately as a _binding_.
- A binding MAY extend the core, but MUST NOT override it. A requirement that more than one binding would need belongs in the core, and one that a single binding needs belongs in that binding.
- A binding SHOULD carry the core's messages as opaque bytes, so that the format native to its transport (e.g., Protocol Buffers in gRPC) never carries the protocol's semantics.
- A new transport MUST be supported through a new binding, rather than a change to the core.

## Exchanges

- Every mechanism in the protocol, including authentication and key agreement, MUST work with the delay, loss, duplication, and reordering of the most constrained transport it must support (e.g., a counter-based one-time password, rather than a time-based one, where messages can arrive days late).
- A message that conveys the outcome of another MUST carry whatever its recipient needs to act on it without having kept the original (e.g., the values requested, alongside those assigned), because timing can't match the two.
- Where the round trip is long, the recipient SHOULD settle a conflict on the sender's behalf and report how it did so, rather than refuse the message (e.g., assign another user name where the one requested is taken).
- Where a recipient needs several messages before it can act, the specification MUST state that their order is irrelevant, and what the recipient does until it has all of them.

## Failures

- What a party is told about a failure MUST be limited to what it needs to act on it (e.g., whether to retry, whose fault the failure is). The diagnosis MUST stay with the party that detected it (e.g., in its logs).
- Where the reason for a refusal would tell the sender something that it mustn't learn (e.g., whether an account exists), the refusal MUST look the same as the outcomes that reveal nothing (e.g., no response at all).
- Each binding MUST say how implementations treat a signal it doesn't define (e.g., an undocumented HTTP status code).

## Interoperability

- Every option that the protocol offers is a way for two conforming implementations to fail to interoperate. Each MUST be justified, and where one choice serves every use case, the protocol MUST mandate it.
- Where a mandatory-to-implement choice will do, a parameter (e.g., a version, an algorithm, a binding) MUST NOT be negotiated. It MUST be mandated by the protocol or declared by the sender in the message, and the recipient MUST refuse what it doesn't support.
- A requirement MUST NOT be added unless what it relies on (e.g., an algorithm) has a production-ready implementation on every platform that the protocol must support, and those implementations interoperate with each other.
- A requirement that proves hard to implement with the mainstream tools of a supported platform SHOULD be reconsidered.

## Wire formats

- Messages SHOULD be serialised in a binary format (e.g., ASN.1 DER, Protocol Buffers).
- A message that's stored, or relayed beyond the hop that delivered it, MUST start with its type and the version of its format, ahead of the encoded content (e.g., a few octets before the DER), so that a later version can change the encoding altogether.

## Limits

- Every limit MUST be an exact number (e.g., in octets, in seconds). Where it's derived from other limits, the specification MUST show the arithmetic (e.g., the largest payload plus the overhead of the fields around it), and where it's arbitrary, the specification MUST say so.
- Where messages carry an expiry date, the protocol MUST cap how far ahead it can be, because that cap bounds what every hop must store, including the records that guard against duplicates.
- Where parties exchange timestamps, the specification MUST state the tolerance for clock skew between each pair of them, according to how well each can keep time (e.g., hours where one can be offline for weeks, none between two servers). The tolerance MUST be applied by whoever checks a timestamp, rather than built into the format.
- A message dated further in the future than that tolerance allows MUST be refused.

## Identifiers

- The specification MUST NOT require implementations to interpret an identifier that they only need to compare (e.g., a certificate serial number), so that they can treat it as an opaque value.
- Where a party is identified by its key, its identifier SHOULD be derived from the key (e.g., a digest of the public key).
- Where a party is identified by a name that people read (e.g., a user name), the protocol MUST constrain the name so that it can't be mistaken for another (e.g., a PRECIS profile, a ban on the character that separates a name from its domain).

## Versioning and extensibility

- Each layer MUST carry its version in the identifier native to it (e.g., an octet in a binary format, a field in a schema, a segment in a URL path, a media type), so that each can evolve independently. An incompatible change MUST get a new identifier, whilst a compatible one MAY keep the existing one.
- A version field MUST always be encoded, even where it holds the initial value (e.g., without a `DEFAULT` in ASN.1).
- An upgrade MUST NOT require every party to upgrade at once: during the transition, recipients MUST accept the previous version alongside the new one. A message whose type or version a recipient doesn't recognise MUST be refused, and MUST NOT cause any other failure.
- Every value that the protocol assigns a meaning to (e.g., a message type, an algorithm identifier) MUST be allocated from a namespace that the protocol's owner controls (e.g., an OID arc, the vendor tree of media types), partitioned so that each protocol has its own branch. Once allocated, a value MUST NOT be reassigned.
- Where third parties can extend the protocol, they MUST allocate the values for their extensions from namespaces of their own.
- Where a value may need to be added or withdrawn without a new version of the protocol (e.g., an algorithm), it MUST be listed in a registry where each entry has a status (e.g., active, deprecated, obsolete), and whose instructions tell whoever reviews an addition what to refuse.
- A value MAY be reserved for an addition that's foreseeable but not yet feasible (e.g., a key type that some supported platforms lack), so that it can arrive without a change to the format.

## Delivery

- Messages that an intermediary could drop selectively to its own advantage (e.g., control messages) MUST travel inside the same encrypted payload as the rest of the traffic, so that it can't tell them apart.
- Where messages are relayed through intermediaries, each MUST carry an identifier that's unique for its sender, so that every hop can recognise a duplicate by the sender and the identifier together.
- The specification MUST say whether a message that reuses the identifier of an earlier one from the same sender is a duplicate to refuse, or a replacement for one still in transit (e.g., a profile picture changed twice in quick succession).

## Privacy

Where privacy is a requirement:

- The protocol MUST be assessed for what each party that handles or observes a message learns from it besides its content (e.g., when it was created, its size, who initiated the exchange, what the recipient asked for). Each leak MUST be mitigated in the protocol itself (e.g., by backdating a timestamp, padding the message, moving a field inside the encrypted payload), or the specification MUST state what the party learns.
- Every identifier and credential that a message exposes MUST be assessed for whether it lets an observer link one party's activity across its peers (e.g., the same intermediate certificate in every message), and SHOULD be left out where it does.
- Privacy requirements on the services that the protocol relies on (e.g., encrypted DNS resolution) MUST be part of the protocol, rather than left to deployment guidance.
- A countermeasure to traffic analysis MUST be assessed for whether it makes the traffic stand out (e.g., padding whose pattern changes with every connection), and against an adversary who controls the component that applies it (e.g., a compromised relay that hands out decoy traffic to see who collects it).

## Additional guidelines

- [Cryptographic protocols](references/cryptographic-protocols.md): The protocol signs, encrypts, or authenticates messages, or issues credentials.
- [Specifications](references/specifications.md): The protocol is being specified, or its specification changed.
