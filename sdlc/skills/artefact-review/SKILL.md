---
name: artefact-review
description: How to review an artefact that you didn't produce, such as a spec, a design, or a change.
---
# Artefact review

## Findings

You MUST check the artefact for findings of each of the following kinds, so that the review is comprehensive:

- Defect: the artefact fails a requirement or a convention.
- Unfit: the artefact meets its requirements, but doesn't solve the underlying problem, possibly because the requirements were wrong or ambiguous.
- Omission: the artefact lacks something that no requirement asks for, but that it needs, possibly because the requirement is missing from the brief.
- Untraced: the artefact has something that you can't trace to a requirement, possibly because the requirement is missing from the brief, or because you missed the connection.

These kinds are for conducting the review, and MUST NOT be relayed in the report.

Each finding MUST state what it is and the consequence of shipping the artefact as it stands. It MUST NOT propose an alternative, except in a cost challenge. A finding that predates the change under review MUST be acknowledged as pre-existing.

## Severity

Each finding MUST be graded by the worst consequence of shipping the artefact as it stands or, for a spec or a design, of building it as specified:

- High: it can do any of the following:
  - Lose or corrupt data, or duplicate it in a way that a user would notice.
  - Expose a secret or personal data.
  - Let someone do what they aren't authorised to (e.g., impersonate another party, get a change through without the required approval).
  - Break backwards compatibility with a system that depends on it.
  - Spend money materially.
  - Impose a material cost on someone who never chose to be a stakeholder, including the environment.
- Medium: the behaviour is wrong, or the finding is in something expensive to reverse once shipped (e.g., an identifier, a wire format, a schema).
- Low: anything else.

## Cost challenge

You MUST challenge the requirements or mechanisms whose cost is highest relative to what they deliver, including any that an earlier round of review added. _Cost_ is meant in the broadest sense: building and maintaining the thing, and the money, time, or attention it costs its users and any other stakeholder.

Each challenge is a finding, graded like any other, and MUST say what dropping or simplifying the requirement or mechanism would save, and what would be lost. There MUST be no more than three challenges, so that they don't lengthen the review much.

## Report

You MUST write the report using the [report template](assets/report.md), leaving out any section that has nothing in it.
