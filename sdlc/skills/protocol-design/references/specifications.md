# Specifications

A specification is written for the implementer who'll get it wrong.

## When to specify

- A protocol MUST be specified before anyone outside the team that designs it implements it. Until then, it MAY be documented informally, provided that the document says it isn't a specification, and when it will become one.
- A change whose cost to implementations is in doubt (e.g., whether its complexity is worth it) SHOULD be prototyped before it's specified.

## Status

- Each specification MUST declare its status (e.g., placeholder, draft, stable, deprecated), which MAY move backwards where it turns out to be less settled than it claimed.
- A specification that is deprecated or abandoned SHOULD be marked as such, rather than deleted.
- A specification MAY be published before it has any requirements, to reserve its identifier and to record its open questions, including whether it's worth having at all.
- A document that nobody is required to comply with MUST say so.
- Each specification MUST link to where it's discussed (e.g., a label in an issue tracker), to any prototype that informed it, and to any reference implementation of it.

## Requirements

- Every requirement MUST be expressed with the keywords of BCP 14 (e.g., MUST, SHOULD, MAY). Guidance that isn't a requirement MUST be marked as non-normative (e.g., in an appendix labelled as such).
- Where an implementer could take a plausible shortcut that breaks a requirement (e.g., deleting a message once it's handed to a relay that may never deliver it), the specification MUST forbid the shortcut explicitly, and give the reason.
- Whatever the specification says about user interfaces (e.g., how to present who vouches for a signature) SHOULD be a recommendation, rather than a requirement.
- Every diagram MUST be published with its source.

## Vocabulary

- Where several specifications form a suite, their terms MUST be defined in one of them, and the others MUST link to those definitions, rather than redefine them.
- Where a name is kept despite being wrong, because changing it would break an identifier or a format, the specification MUST explain it.

## Sections

- Security considerations and privacy considerations MUST be separate sections. The privacy considerations MUST state what each party learns, including whatever the protocol can't keep from it.
- The specification MUST state the protocol's limitations, including any use that it can't serve (e.g., one-way communication).
- Where the specification departs from what's already deployed, it MUST list each departure.
- Any conflict of interest of its authors (e.g., leading an implementation, maintaining a competing protocol) MUST be declared.
