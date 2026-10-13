# Cryptographic protocols

## Algorithms

- In each category (e.g., hashing, signing, key agreement, symmetric encryption), the protocol MUST allow a closed set of algorithms, and implementations MUST refuse any other.
- Exactly one algorithm in each category SHOULD be mandatory to implement. Others MAY be allowed alongside it, for those who need stronger guarantees than it offers.
- Broken or weak algorithms that implementations might still support (e.g., SHA-1, RSA keys under 2048 bits) MUST also be banned by name.
- These rules MUST extend to the algorithms that another algorithm uses internally (e.g., the hash function in a key derivation function).

## Verification

- Where a security property depends on a third party's answer (e.g., a DNS record), implementations MUST authenticate the answer themselves (e.g., by validating DNSSEC), rather than trust whoever relayed it (e.g., a resolver).
- Where the input to a verification admits more than one interpretation (e.g., two records that match the same key), verification MUST fail.
- Verification MUST be specified as a procedure that implementations perform in full, with no step that they may skip.

## Credentials and signatures

- The protocol MUST cap how long a credential can be valid, as low as its use cases allow, because wherever verifiers can't check for revocation, a compromised key remains usable until its credentials expire.
- Rotating a key or a credential MUST NOT require the parties to switch at the same time (e.g., verifiers accept every credential that's still valid, a recipient keeps its previous key for a grace period).
- Where a credential binds a name that isn't derived from a key (e.g., a user name under a domain), its issuer MUST only be able to certify the names that it controls.
- A certificate MUST NOT be used where a raw key would do (e.g., an ephemeral key that the message carrying it already authenticates).
- Where intermediaries must enforce an authorisation without reading the content, it SHOULD be expressed as a credential issued by the party granting it (e.g., a recipient certifying a sender).
- Every signature MUST be bound to its purpose, through an identifier of the purpose in the signed content (e.g., an OID per message type), and verifiers MUST refuse a signature made for another purpose. Where a signature is meant for one recipient, it MUST also be bound to that recipient (e.g., through an audience).

## Building on other work

- Where the protocol adapts a published one, the specification MUST list every deviation, with its reason, and the limitations that result (e.g., a use that it can't serve).
- Where no standard fills a gap, the invention MUST be the smallest that fills it, and the specification MUST say which gap that is.
