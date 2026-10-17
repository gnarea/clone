---
name: artefact-review
description: How to review an artefact, whatever the discipline. Findings, their severity, the cost challenge, and the feedback template. Use when reviewing any artefact, such as a spec, a design, or a change.
---
# Artefact review

## Findings

You MUST flag every finding, and label it as one of the following:

- Defect: the artefact fails a requirement or a convention.
- Mismatch: the artefact meets its requirements, but solves a different problem from the one it was meant to.
- Addition: the artefact would need something that no requirement asks for. Additions aren't graded, and don't block the artefact.

Each defect and mismatch MUST state what's wrong and the consequence of shipping it, without proposing an alternative. A defect that predates the change under review MUST be marked as pre-existing.

## Severity

Each defect and mismatch MUST be graded by the worst consequence of shipping it or, for a spec or a design, of building it as specified:

- High: it can do any of the following:
  - Lose or corrupt data, or duplicate it in a way that a user would notice.
  - Expose a secret or personal data.
  - Let someone do what they aren't authorised to (e.g., impersonate another party, get a change through without the required approval).
  - Break backwards compatibility with a system that depends on it.
  - Spend money materially.
  - Impose a material cost on someone who never chose to be a stakeholder, including the environment.
- Medium: the behaviour is wrong, or it's in something expensive to reverse once shipped (e.g., an identifier, a wire format, a schema).
- Low: anything else.

## Cost challenge

You MUST challenge the requirements or mechanisms whose cost is highest relative to what they deliver, including any that an earlier round of review added. _Cost_ is meant in the broadest sense: building and maintaining the thing, and the money, time, or attention it costs its users and any other stakeholder.

The challenge MUST cover no more than three of them, so that it doesn't lengthen the review much. Each MUST take one line, saying what dropping or simplifying it would save, and what would be lost.

## Template

You MUST give your feedback using the following template, leaving out any section that has nothing in it:

```markdown
# Findings

## High

- (Defect, pre-existing defect, or mismatch): (What's wrong, and the consequence of shipping it.)

## Medium

(As above.)

## Low

(As above.)

## Additions

- (What the artefact would need, and why.)

# Cost challenge

- (Requirement or mechanism): (What dropping or simplifying it would save, and what would be lost.)
```
