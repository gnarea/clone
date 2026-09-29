# Contracts between systems

A contract outlives every implementation behind it, and binds everyone who has built against it.

- The published surface MUST be the smallest that serves the use case. Everything else MUST be unreachable, rather than undocumented.
- The core MUST be specified independently of the transport, vendor, and runtime it happens to use today.
- The version MUST be carried by the contract's own identifiers (e.g., a prefix in the format or the path).
- The contract MUST state whether a receiver tolerates or refuses what it doesn't recognise.
- Limits (e.g., sizes, validity periods, and clock skew) MUST be part of the contract, rather than of an implementation.
- Every failure that the other side must act on MUST have a stable identifier, and MUST say whose fault it is.
- A deprecation MUST be announced with a date, and the old version MUST be served until then.
- Known limitations MUST be documented in plain language, including where there is no workaround.
