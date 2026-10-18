---
name: artefact-review
description: How to review an artefact that you didn't produce, such as a spec, a design, or a change, and how to process feedback on an artefact that you produced.
---
# Artefact review

## Severity

Each finding MUST be graded by the worst consequence of shipping the artefact as it stands or, for a spec or a design, of building it as specified:

- High: the artefact MUST NOT be shipped until the finding is addressed. This includes, but isn't limited to, any case where the artefact can:
  - Lose or corrupt data, or duplicate it in a way that a user would notice.
  - Expose a secret or personal data.
  - Let someone do what they aren't authorised to (e.g., impersonate another party, get a change through without the required approval).
  - Break backwards compatibility with a system that depends on it.
  - Impose a material cost on a stakeholder.
- Medium: the artefact SHOULD NOT be shipped until the finding is addressed. This includes, but isn't limited to, any case where the behaviour is wrong, or where the finding is in something expensive to reverse once shipped (e.g., an identifier, a wire format, a schema).
- Low: the artefact MAY still be shipped despite the finding.

## Additional guidelines

- [Reviewing an artefact](references/reviewing.md): You're reviewing an artefact that you didn't produce.
- [Processing feedback](references/processing-feedback.md): You've received feedback on an artefact that you produced.
