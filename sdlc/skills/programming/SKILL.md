---
name: programming
description: Principles and conventions when implementing or reviewing code changes.
---
# Programming

Before writing or reviewing code, you MUST read the references covering the aspects that the change touches:

- `references/naming.md`: Naming anything: a file, type, function, field, constant, or test case.
- `references/structure.md`: Adding or moving a file, or writing a function of any length.
- `references/data-model.md`: Defining a type, or accepting a value that originates outside the module.
- `references/errors.md`: A failure path: raising, catching, returning, or logging a failure.
- `references/testing.md`: Writing or reviewing a test, or changing a quality gate.

## Additional, generally-applicable guidelines

### Prose

Prose in identifiers, comments, documentation, and log messages MUST observe the ghost-writing skill.

### Comments

- You MUST NOT add or augment code comments, unless the rationale for a particular block of code could not be inferred by carefully analysing the surrounding code. Typically, that means a workaround for an upstream bug (with a link to it), a spec ambiguity resolved one way, the derivation of a non-obvious constant, a deliberate trade-off, or the absence of code that a reader would expect to find.
- All public or exported members of **published libraries** MUST have appropriate doc comments.
- All comments MUST be succinct and avoid references to specific files/lines in the project.
- `TODO`, `FIXME`, and `HACK` markers MUST NOT be committed. Track the work in the issue tracker instead.
