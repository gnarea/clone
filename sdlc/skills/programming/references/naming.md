# Naming

- All identifiers (e.g., function names) MUST be self-explanatory and concise. Additionally, they SHOULD match the taxonomy of the user and/or programming interfaces.
- Constants, variables, fields, and the like, SHOULD be named after what they hold, rather than what they are used for.
- Functions, procedures, and the like, MUST be written in imperative form (e.g., `submitResult`) or as questions (e.g., `wasResultSubmitted`).
- Booleans, and the functions that return them, MUST be prefixed with `is`, `has`, `are`, `can`, `do`/`does`/`did`, `should`, or `was`/`were`.
- Verbs MUST be used consistently across the codebase. For example: `make*` for factories, `init*` for constructors that read their input from the environment or a serialised form, `register*` for plugins, `configure*` for process-level side effects, and `require*` for guards that return nothing.
- `serialise`/`deserialise` MUST denote conversions to and from bytes, `encode`/`decode` those to and from structured representations, and `parse` those from strings.
- Generic type parameters MUST be whole words (e.g., `ResultType`), never single letters.
- Abbreviations MUST NOT be invented (e.g., `index`, not `i`). Only those already established in the domain or the platform MAY be used.
