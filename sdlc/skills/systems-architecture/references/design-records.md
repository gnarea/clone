# Design records

## The architecture document

Each product MUST have a standing architecture document that every change is judged against, and a change MUST amend it rather than leave it for later. It MUST cover:

- The components, what each knows, and whom each trusts with what.
- The contracts between them, and with the systems they depend on or serve.
- What each component stores, and for how long.
- The most constrained environment the system must run in.
- The threat model, including the residual risks.
- The non-goals, and the deferred decisions.

## Proposing a change

A change MUST be proposed in the issue tracker, following the /ghost-writing:issue-tracking skill, with these sections instead of the generic ones:

```markdown
# Summary

(For a technical reader who doesn't know the domain's vocabulary.)

# Problem

(With no solution in it. Where a requirement is questioned, say why it was believed to be necessary.)

# Proposed design

(What changes, component by component, and which parts of the architecture document it amends.)

# Trade-offs

(What this optimises for, at the expense of what, and the second-order consequences.)

# Alternatives considered

(Each one, and why it was rejected.)

# Non-goals

# Residual risks

(What remains after the change, including what would defeat each mitigation.)

# Ethical considerations

(Who is worse off if this succeeds, including people who aren't users, and the environmental cost.)

# Open questions

(Each one, next to the decision it blocks.)
```

## Arguing for a reversal

Where a proposal drops a requirement or reverses a decision, it MUST:

1. Restate the current design in its own best terms.
2. Say what was wrong with the original requirement, on its own terms.
3. Enumerate every simplification that the reversal buys.
4. Enumerate the consequences being accepted, and say why the advantages still outweigh them.

## Closing

An issue MUST be closed with the argument that settled it, including where the argument is that nothing was found to justify a change.
