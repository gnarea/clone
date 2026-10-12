# Specifications

A specification is written for the implementer who'll get it wrong.

## When to specify

- A protocol MUST be specified before anyone outside the team that designs it implements it. Until then, it MAY be documented informally, provided that the document says it isn't a specification, and when it will become one.
- A change whose cost to implementations is in doubt (e.g., whether its complexity is worth it) SHOULD be prototyped before it's specified.

## Status

- Each specification MUST declare its status (e.g., placeholder, draft, stable, deprecated), which MAY move backwards where it turns out to be less settled than it claimed.
- A specification that is deprecated or abandoned MUST be marked as such, rather than deleted, and its identifier MUST NOT be reused.
- A specification MAY be published before it has any requirements, to reserve its identifier and to record its open questions, including whether it's worth having at all.
- A document that nobody is required to comply with MUST say so.
- Each specification MUST link to where it's discussed (e.g., a label in an issue tracker), to any prototype that informed it, and to its reference implementations.

## Requirements

- Every requirement MUST be expressed with the keywords of BCP 14 (e.g., MUST, SHOULD, MAY). Anything else MUST be marked as non-normative (e.g., an appendix labelled as such).
- Where an implementer could take a plausible shortcut that breaks a requirement (e.g., deleting a message once it's handed to a relay that may never deliver it), the specification MUST forbid the shortcut by name, and give the reason.
- Requirements on what implementations show to users SHOULD be recommendations, because the specification can't foresee every interface.
- Each format MUST have a single normative definition in a machine-readable notation (e.g., an ASN.1 module, a `.proto` file), included in the specification from its source file, rather than restated in prose.
- Every diagram MUST be published with its source.
- Until the specification is submitted to a standards body, it MAY declare that its reference implementations settle any ambiguity in it. From then on, the text alone MUST be normative.

## Vocabulary

- Where several specifications form a suite, their terms MUST be defined in one of them, and the others MUST link to those definitions, rather than redefine them.
- Where a name is kept despite being wrong, because changing it would break an identifier or a format, the specification MUST explain it.

## Sections

- Security considerations and privacy considerations MUST be separate sections. The privacy considerations MUST state what each party learns, including whatever the protocol can't keep from it.
- Limitations MUST have a section of their own, including any use that the protocol can't serve (e.g., one-way communication).
- Each alternative considered (e.g., a standard, a competing protocol) MUST be recorded with the specific reason that it was rejected, in terms that could be proven wrong.
- Where the protocol has implementations, the specification SHOULD list each one with its maturity, and every point where the specification departs from what's deployed. Any conflict of interest of its authors (e.g., leading an implementation, maintaining a competing protocol) MUST be declared.
- The specification MUST keep a changelog, including the decisions it reverses.
- Open questions MUST be published in the specification itself, next to the decision they block. Those about the specification as a whole MUST be in a section of their own, at the end.
