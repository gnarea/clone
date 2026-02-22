---
name: ghost-writing
description: How I strive to write. Apply these conventions when drafting or editing any text on my behalf.
user-invocable: false
---

Determine whether the context is **formal** (specs, RFDs, Internet-Drafts), **semi-formal** (blog posts, issue/PR descriptions, documentation), or **informal** (chat messages, issue/PR comments), then apply the core rules plus the relevant context section below. When in doubt, ask.

## Core Rules

- **Tone**: friendly and approachable, but factual and objective in substance.
- **Density**: information-packed. No filler words (e.g., "basically", "actually", "just", "really", "very"), no repetition. Every sentence earns its place.
- **Clarity**: articulate. Present ideas so they are immediately clear to the reader.
- **Concreteness**: ground explanations in specific examples and scenarios rather than abstract descriptions.
- **Honesty**: state assumptions, constraints, and uncertainty directly rather than overstating confidence.
- **Layered exposition**: definitions before examples, with links as escape hatches for depth.
- **Parallelism**: use consistent grammatical structure across list items and comparable elements.
- **Voice**: prefer active voice.
- **Oxford comma**: always.
- **List items**: always end with punctuation (typically a full stop).
- **Blank lines**: always include a blank line before and after list blocks.

## British English

- Proper nouns and pre-existing identifiers (`background-color`, `gray` in CSS, `center` in HTML) remain in American English. Example: software licences like "MIT License".
- Default to `-ise` for all `-ise`/`-ize` variants (serialise, normalise, initialise, optimise, synchronise, authorise, customise, analyse).
- Doubled consonants before suffixes: modelling, labelling, cancelling, travelling.
- Key vocabulary: behaviour, colour, centre, defence, licence (noun) / license (verb), grey, fulfil, spelt (not "spelled").
- Always "whilst" as a conjunction, not "while" (except where grammatically required: "once in a while", "while away the time").
- *Programme* for non-software contexts (training programme, conference programme); *program* for software.
- No full stop after abbreviations: Dr, Mr, Mrs, vs (not Dr., Mr., Mrs., vs.).
- Dates: DD Month YYYY (e.g., 22 February 2026). Never MM/DD/YYYY.
- Times: 24-hour format without leading zero (e.g., 9:00, 17:30).

**Do this, not this:**

- "The system serialises the data." not "The system serializes the data."
- "Whilst the build runs, review the logs." not "While the build runs, review the logs."
- "22 February 2026" not "February 22, 2026".
- "The meeting is at 14:30." not "The meeting is at 2:30 PM."
- "Mr Narea" not "Mr. Narea".

## Formatting

Use the richest options the medium supports.

**Text emphasis** (where supported):

- *Italics*: for introducing a term for the first time in a given text.
- **Bold**: for emphasis. Use sparingly for maximum impact.
- Backticks: for software identifiers (e.g., `background-color`, `serialise_data`) and inline code.

**Links and URLs** — use the richest format the medium supports, degrading gracefully:

- Markdown-capable contexts (specs, docs, GitHub): `[text](url)`.
- Rich-text platforms (Slack, etc.): platform-native link syntax.
- Plain text, formal (professional email): footnote-style references ("see [1]", URLs listed at end).
- Plain text, informal (quick message): inline URLs.

## Informal Writing (e.g., chat messages, issue/PR comments)

In addition to the core rules:

- Contractions encouraged (don't, isn't, I've, haven't, etc.).
- British colloquial constructions: "I've got X", "I haven't got X", "have you got X?".
- No em-dashes.
- Emojis sparingly — only to convey or emphasise emotions.

**Do this, not this:**

- "I've got a question about this." not "I have a question about this."

## Semi-Formal Writing (e.g., blog posts, issue/PR descriptions, documentation)

In addition to the core rules:

- Contractions allowed.
- Em-dashes permitted (sparingly).
- No emojis.
- [See blog post exemplar](https://awala.app/en/blog/2025-01-06-internet-censorship-future/).

## Formal Writing (e.g., specs, RFDs, Internet-Drafts)

In addition to the core rules:

- No contractions.
- Em-dashes permitted (sparingly).
- No emojis.
- Formal but accessible tone.
- [See DomainAuth I-D exemplar](https://github.com/CheVeraId/domainauth-spec).
