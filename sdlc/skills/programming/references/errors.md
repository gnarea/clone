# Failure paths

## Errors

- Failures that the caller is expected to reason about MUST be returned as values (e.g., a result type carrying the reason). Programming errors and protocol violations MUST be raised.
- Raised errors MUST derive from a single root type owned by the module, so that a caller can catch everything the module owns, and nothing it doesn't.
- The cause MUST always be chained. Discarding one MUST be syntactically deliberate.
- Third-party errors MUST NOT escape the module that provoked them: catch them, and re-raise them in the module's own vocabulary.
- The documentation of each error type MUST tell the caller what to do about it, starting with whether retrying is likely to help.
- Messages MUST state the expectation and the offending value (e.g., "TTL exceeds the maximum (got 3600)"), and MUST NOT carry secrets or personal data.
- Where tests assert on messages, the wording is API surface, and MUST be changed as deliberately as any other part of it.

## Logging

- Logs MUST be structured: the message is a constant string, and everything variable is a field.
- The level MUST encode fault attribution: the caller's fault is `info`, ours is `warn` or `error`, and anything the operator isn't expected to act upon is `debug`.
- Personal data MUST NOT be logged above `debug`, and secrets MUST NOT be logged at all.
- Log volume MUST be treated as a cost borne by the operator. For example, log the reason for a failure rather than the entire error, when the reason suffices.
