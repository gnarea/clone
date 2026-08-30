# API design

The contract is the product: it outlives every implementation behind it, so the investment goes into the surface.

## Any contract

- The public surface MUST be the smallest one that serves the use case. Anything else MUST be internal, and MUST be made unreachable rather than merely undocumented.
- Extension MUST happen through a named extension point (e.g., a binding, or a registry), never by revising the core contract. An extension MAY add to the core, but MUST NOT override it.
- Versioning and extensibility MUST be designed in from the first release, rather than retrofitted once a second consumer exists.
- Every contract MUST state its non-goals, and SHOULD state which gaps we would accept contributions for.
- Where an algorithm or a mode is negotiable, the mandatory-to-implement set MUST be specified, and unsafe options MUST be inexpressible rather than merely discouraged.

## Published libraries

- The surface MUST be explicit at the language level (e.g., an explicit API mode), so that adding to it is a deliberate act rather than an accident of visibility.
- A type that callers must be able to reference, but not instantiate or extend, MUST be sealed at the module boundary (e.g., a public abstract class with an internal constructor).
- Anything that can fail MUST be exposed as a named factory rather than a constructor, drawn from a small closed vocabulary (e.g., `init`, `initFrom*`, `deserialise`, `generate`).
- Validation that an implementor must not skip MUST be enforced by the library, not delegated to whoever implements the extension point.
- Test doubles that consumers will need MUST ship as part of the library, and MUST be held to the same quality gates as the rest of it.
- Portability MUST be tested against everything the library claims to support: every operating system, runtime version, and platform API level.
- Where testability requires widening visibility, the concession MUST be documented at the declaration.
