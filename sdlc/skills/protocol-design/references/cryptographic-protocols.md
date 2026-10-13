# Cryptographic protocols

## Algorithms

- In each category (e.g., hashing, signing, key agreement, symmetric encryption), the protocol MUST allow a closed set of algorithms, as small as interoperability allows, and every implementation MUST support all of it. It MAY also define an optional set of stronger alternatives, for environments that need better security or privacy guarantees.
- Algorithms that the specification doesn't allow MUST be refused. Broken or weak ones that implementations might still support (e.g., SHA-1, RSA keys under 2048 bits) MUST also be banned by name.
- Where the set of algorithms must be able to change without a new version of the protocol, it MUST be a registry (per the rules on versioning and extensibility), in which a mandatory algorithm can itself be deprecated.

## Verification

- Where a security property depends on a third party's answer (e.g., a DNS record), implementations MUST authenticate the answer themselves (e.g., by validating DNSSEC), rather than trust whoever relayed it (e.g., a resolver).
- Where the input to a verification admits more than one interpretation, verification MUST fail.
- Verification MUST be specified as a procedure that implementations perform in full, with no step that they may skip.
- Rotating a key or a credential MUST NOT require the parties to switch at the same time (e.g., verifiers accept every credential that's still valid, a recipient keeps its previous key for a grace period).

## Credentials and signatures

- Credentials MUST be as short-lived as possible.
- Where a credential binds a name that isn't derived from a key (e.g., a user name under a domain), its issuer MUST only be able to certify the names that it controls.
- A certificate MUST NOT be used where a raw key would do (e.g., an ephemeral key that the message carrying it already authenticates).
- Every signature MUST be bound to its purpose, through an identifier of the purpose in the signed content (e.g., an OID per message type), and verifiers MUST refuse a signature made for another purpose. Where a signature is meant for one recipient, it MUST also be bound to that recipient (e.g., through an audience).

## Building on other work

- Where the protocol adapts a published one, the specification MUST list every deviation, with its reason, and the limitations that result (e.g., a use that it can't serve).
- Where no standard fills a gap, the invention MUST be the smallest that fills it, and the specification MUST say which gap that is.
