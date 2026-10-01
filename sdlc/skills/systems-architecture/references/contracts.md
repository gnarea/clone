# Contracts between systems

A contract outlives every implementation behind it, and binds everyone who has built against it.

- The published interface MUST be the smallest that serves the use case. Everything else MUST be unreachable, rather than undocumented.
- The core MUST be specified independently of the transport, vendor, and runtime it happens to use today.
- The contract MUST evolve by addition, and breaking changes MUST be avoided. Where one can't be (e.g., to fix a correctness or security defect), it MUST ship as a new major version.
- Identifiers and serialisation formats that outlive any one message (e.g., addresses and key formats) MUST carry a version (e.g., a prefix).
- Limits (e.g., sizes, validity periods, and clock skew) MUST be part of the contract, rather than of an implementation.
- Where clients can't be upgraded in step with the server (e.g., apps already installed), every abuse control that the threat model calls for MUST be in the contract's first version, even at a setting that demands nothing (e.g., a challenge of zero difficulty), because adding one later locks out existing clients.
- Every failure that the other side must act on MUST have a stable identifier, and MUST say whose fault it is.
