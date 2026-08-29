# Data model

## Types

- Illegal states MUST be unrepresentable. A parameter that selects between behaviours MUST be an enum or a set of named factories, never a boolean; a value drawn from a closed set MUST be an enum, never a string.
- Invariants MUST be enforced where the value is constructed, so that an invalid instance cannot exist. Deserialisers MUST validate before constructing.
- Types MUST be immutable by default. Mutability MUST be confined to where it's needed, and MUST be evident in the type.
- Every literal with meaning MUST be a named constant, and its unit MUST be part of the name (e.g., `TOKEN_TTL_MINUTES`).
- Identifiers exposed to third parties MUST NOT be guessable, and MUST NOT leak the time or the volume of what they identify (e.g., a UUIDv4, rather than a sequential or timestamp-derived database id).

## Trust boundaries

- Input crossing a trust boundary MUST be validated before use. This includes the responses of dependencies we operate ourselves.
- Every untrusted input MUST have an explicit size limit, and every outbound call MUST have a timeout. Both MUST be named constants, with a comment deriving the figure.
- Where the configuration is ambiguous or incomplete, the code MUST fail closed and refuse to start, rather than guess an apparently safe default.
- Defence in depth MUST be applied wherever it's cheap. For example, validate a value both when it's issued and when it's verified.
