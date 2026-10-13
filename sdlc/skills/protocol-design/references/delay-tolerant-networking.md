# Delay-tolerant networking

In a delay-tolerant network, intermediaries store messages and forward them later (aka _store and forward_), so a message can take days to arrive, and its recipient may be offline when it does.

## Exchanges

- Whatever runs across the network, rather than over a single live connection, MUST NOT rely on synchronised clocks, nor on a challenge from the other party (e.g., a counter-based one-time password, rather than a time-based one).
- A message that conveys the outcome of another MUST identify the one it answers (e.g., by its identifier), because timing can't match the two.
- The recipient SHOULD settle a conflict on the sender's behalf and report how it did so, rather than refuse the message (e.g., assign another user name where the one requested is taken), because a refusal costs another round trip.

## Intermediaries

- Each message MUST carry an identifier that's unique for its sender until the message expires. An intermediary MUST authenticate the sender before treating a message as a duplicate of another, or as its replacement.
- The specification MUST say whether a message that reuses the identifier of an earlier one from the same sender is a duplicate to refuse, or a replacement for one still in transit (e.g., a profile picture changed twice in quick succession).
- An intermediary that isn't trusted MUST NOT be able to replay a message undetected (e.g., a sequence number inside the encrypted message, which the response echoes).
- A session between the parties at either end SHOULD outlive the connection that carries it, so that it can resume through another intermediary.
- A requirement MUST NOT be added unless the third-party software that messages pass through (e.g., a reverse proxy) already supports what it relies on.
- Where intermediaries must enforce an authorisation without reading the content, it SHOULD be expressed as a credential issued by the party granting it (e.g., a recipient certifying a sender).

## Verification

- The protocol MUST NOT depend on an online authority to verify a message, including for revocation, and every message MUST carry whatever its verifier needs and doesn't already hold (e.g., the certificate chain).
- A credential's validity period MUST allow for how long messages take to arrive, so "as short-lived as possible" can mean weeks or months.
- Verification MUST take the period of interest as an input (e.g., any time in the last 30 days), because a message may be verified long after it was produced. Everything that the verification relies on (e.g., credentials, signatures) MUST have been valid at the same time, at some point within that period.
