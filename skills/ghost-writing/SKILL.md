---
name: ghost-writing
description: How Gus strives to write. Apply these conventions when drafting or editing text on his behalf.
user-invocable: false
---

Determine the formality of the context, then apply the core rules plus the relevant subsection below. When in doubt, ask.

## Core Rules

- Friendly and approachable in tone, but factual and objective in substance.
- Information-dense: no filler words (e.g., "basically", "actually", "just", "really", "very"), no repetition. Every sentence earns its place.
- Present ideas so they land immediately.
- Ground explanations in specific examples and scenarios, not abstract descriptions.
- State assumptions, constraints, and uncertainty directly, rather than overstating confidence.
- Definitions before examples, with links as escape hatches for depth.
- Consistent grammatical structure across list items and comparable elements.
- Active voice preferred.
- Oxford comma always.
- List items end with a full stop (or other terminal punctuation).
- Blank line before and after every list block.

## Nomenclature

- _Internet_ (capital I) for the global network; _internet_ (lowercase i) for a generic network of networks.
- _Web_ (capital W) for the World Wide Web.

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

- "The organisation's modelling of programme behaviour spans three centres, with results serialised on 22 February." not "The organization's modeling of program behavior spans three centers, with results serialized on February 22."
- "Whilst analysing the grey colour scheme, the defence team realised the licence had lapsed." not "While analyzing the gray color scheme, the defense team realized the license had lapsed."

## Formatting

Use the richest options the medium supports.

**Text emphasis** (where supported):

- _Italics_: for introducing a term for the first time in a given text. Use underscores (`_text_`), not asterisks.
- **Bold**: for emphasis. Use sparingly for maximum impact.
- Backticks: for software identifiers (e.g., `background-color`, `serialise_data`) and inline code.

**Links and URLs** — use the richest format the medium supports, degrading gracefully:

- Markdown-capable contexts (specs, docs, GitHub): `[text](url)`.
- Rich-text platforms (Slack, etc.): platform-native link syntax.
- Plain text, formal (professional email): footnote-style references ("see [1]", URLs listed at end).
- Plain text, informal (quick message): inline URLs.

## Formality

### Informal

Applies to chat messages, issue/PR comments, and similar casual contexts.

- Contractions encouraged (don't, isn't, I've, haven't, etc.).
- British colloquial constructions: "I've got X", "I haven't got X", "have you got X?".
- No em-dashes.
- Emojis sparingly — only to convey or emphasise emotions.

**Do this, not this:**

- "I've got a question about this." not "I have a question about this."

### Semi-Formal

Applies to blog posts, issue/PR descriptions, documentation, and similar contexts.

- Contractions allowed.
- Em-dashes permitted (sparingly).
- No emojis.
- [See blog post exemplar](https://awala.app/en/blog/2025-01-06-internet-censorship-future/).

### Formal

Applies to specs, RFDs, Internet-Drafts, and similar contexts.

- No contractions.
- Em-dashes permitted (sparingly).
- No emojis.
- Formal but accessible tone.
- [See DomainAuth I-D exemplar](https://raw.githubusercontent.com/CheVeraId/domainauth-spec/main/draft-narea-domainauth.md).
