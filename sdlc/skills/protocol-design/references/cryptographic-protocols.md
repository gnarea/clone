# Cryptographic protocols

## Algorithms

- In each category (e.g., hashing, signing, key agreement, symmetric encryption), the protocol MUST mandate exactly one algorithm that every implementation supports. It MAY recommend others that are stronger, but costlier or less widely available.
- Each algorithm MUST be stated with how long it's assumed to stay secure (e.g., until 2030), so that the assumption can be revisited.
- Algorithms that the specification doesn't allow MUST be refused. Broken or weak ones that implementations might still support (e.g., SHA-1, RSA keys under 2048 bits) MUST also be banned by name.
- The output of a key agreement MUST NOT be used as a key: it MUST go through a key derivation function, which is subject to the same rules as every other algorithm.
- Where the set of algorithms must be able to change without a new version of the protocol, it MUST be a registry (per the rules on versioning and extensibility), in which the mandatory algorithm can itself be deprecated.

## Verification

- Where verification must work without contacting anyone (e.g., offline), every message MUST carry everything needed to verify it (e.g., the certificate chain, the DNSSEC chain), and the protocol MUST NOT depend on an online authority, including for revocation.
- Where revocation can't be checked, credentials MUST have a short maximum validity period instead, and the specification MUST list as a limitation that a compromised key remains usable until its credential expires.
- Every constraint that the protocol places on issuers (e.g., the maximum validity period, the syntax of a name) MUST also be enforced by verifiers, so that a lax issuer can't reintroduce the risk it guards against.
- Where a message may be verified long after it was produced, verification MUST take the period of interest as an input (e.g., any time in the last 30 days), and MUST require every credential and signature in the chain to have been valid simultaneously at some point within it.
- Where the protocol relies on a third party's answer (e.g., a DNS record), implementations MUST authenticate the answer themselves (e.g., by validating DNSSEC), rather than trust whoever relayed it (e.g., a resolver).
- Where the input to a verification admits more than one interpretation (e.g., two records match), verification MUST fail. Where it relies on a set of authenticated answers, the protocol MUST fix how many there are (e.g., exactly one TXT record), so that an implementation can't read a value from an answer that wasn't authenticated.
- Verification MUST be specified as a procedure that implementations perform in full, with no step that they may skip.
- Key rotation MUST NOT require the parties to switch at the same time: new signatures MUST use the credential that expires last, and verifiers MUST accept every credential that's still valid.

## Credentials and signatures

- An issuer MUST only be able to certify the names that it controls (e.g., an organisation certifying only the members of its own domain).
- Where intermediaries must enforce an authorisation without reading the content, it SHOULD be expressed as a credential issued by the party granting it (e.g., a recipient certifying a sender).
- A certificate MUST NOT be used where a raw key would do (e.g., an ephemeral key that the message carrying it already authenticates).
- Every signature MUST be bound to its purpose, through an identifier of the purpose in the signed content (e.g., an OID per message type), and verifiers MUST refuse a signature made for another purpose. Where a signature is meant for one recipient, it MUST also be bound to that recipient (e.g., through an audience).

## Building on other work

- Where the protocol adapts a published one, the specification MUST list every deviation, with its reason, and every security property of the original that the adaptation lacks (e.g., forward secrecy).
- Where no standard fills a gap, the invention MUST be the smallest that fills it, and the specification MUST say which gap that is.
- A protocol with security or privacy properties SHOULD be assessed by an independent party from its specification alone, before it's implemented, and again once it has been, including the dependencies that those properties rely on. Where the specification is public, the reports MUST be published in full, along with the recommendations that weren't acted on.
