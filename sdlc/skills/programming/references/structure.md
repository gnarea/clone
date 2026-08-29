# Code structure

## Code organisation

- Modules MUST be partitioned by responsibility, using whichever decomposition is idiomatic for the software and its stack (e.g., layers such as domain, data, and UI in an application; capabilities in a library). Whichever is chosen MUST be applied uniformly, and MUST be documented in the README.
- Each file MUST expose at most one public/exported type. Cohesive families (e.g., an error hierarchy) MAY share a file.
- Files SHOULD NOT span more than 800 LOC, including comments and new lines. 1 kLOC or more SHOULD be deemed a code smell.
- Everything that isn't part of a module's contract MUST use the strictest visibility the language offers.
- A library's public surface MUST be declared explicitly in a single, hand-curated entrypoint. Wildcard re-exports MUST NOT be used.
- Entrypoints (e.g., `main`) MUST contain no logic of their own: they wire dependencies together and delegate.

## Functions, procedures, and the like

- Each MUST do one thing, at one level of abstraction. They SHOULD NOT exceed 40 LOC, nor a cyclomatic complexity of 10.
- Guard clauses and early returns MUST be preferred over nesting. An `else` on a failure path is a code smell.
- Parameter lists SHOULD NOT exceed seven parameters. Beyond that, the parameters MUST be grouped into a type that names their relationship.
- Anything that can fail MUST NOT be exposed as a constructor: use a named factory instead (e.g., `deserialise`, `generate`).
- Validation that an implementor must not skip MUST be enforced in a final public method that delegates to a protected hook, rather than left to each implementation.
- Inequalities SHOULD be ordered, with `<`/`<=` preferred over `>`/`>=` so that operands read from lower to upper bound (e.g., `if (ttl < MAX_TTL_SECONDS)`, `if (MIN_TTL_SECONDS <= ttl && ttl <= MAX_TTL_SECONDS)`).
