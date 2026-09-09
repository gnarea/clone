# Design records

## The product's architecture document

Each product MUST have a standing architecture document, kept current, that a change is judged against. It MUST cover:

- The components, and what each one is allowed to know.
- The contracts between them, and with the systems they depend on or serve.
- What each component stores, and for how long.
- The threat model, including the residual risks.
- The non-goals, and the deferred work with the criteria that would bring it forward.

A change request MUST cite the parts of it that the change contradicts or amends, and the document MUST be amended as part of the change rather than afterwards.

## Proposing a change

An architectural change MUST be proposed in the issue tracker, following the /ghost-writing:issue-tracking skill for tone and structure, with these sections instead of the generic ones:

```markdown
# Summary

(A few sentences for a technical reader who does not know this domain's vocabulary.)

# Problem

(The problem in its own terms, with no solution in it. Where a requirement is being questioned, say why it was believed to be necessary.)

# Proposed design

(What changes, component by component, and which parts of the architecture document it amends.)

# Alternatives considered

(Each one, with why it was rejected. Mandatory: a proposal that names no alternatives is incomplete.)

# Non-goals

(What this deliberately does not address.)

# Limitations and residual risks

(What remains true after the change, including what would defeat each mitigation.)

# Collateral damage and ethical considerations

(Optional; who is worse off if this succeeds, including people who are not our users.)

# Open questions

(What is unresolved, next to the decision it blocks.)
```

## Arguing for a reversal

Where the proposal drops a requirement or reverses an earlier decision, it MUST take this shape:

1. Restate the current design in its own best terms.
2. Say what was wrong with the original requirement, on its own terms.
3. Enumerate the whole cascade of simplifications that dropping it buys.
4. Enumerate the unintended consequences being accepted, and say why the advantages still outweigh them.

## Recording the outcome

- A losing option MUST keep its identifier and its reasoning, marked as rejected, deprecated, or abandoned. It MUST NOT be deleted.
- An issue MUST be closed with the argument that settled it, including where that argument is that nothing was found to justify the change.
- Decisions MUST be indexed by what caused them as well as by what they touch, so that everything a given dependency, quality attribute, or threat forced on the design can be found at once.
