---
name: ghost-writing
description: How Gus strives to write. Apply these conventions when drafting or editing text on his behalf.
user-invocable: false
---

Determine the formality of the context, then apply the core rules plus the relevant subsection below. When in doubt, ask.

## Core Rules

- Friendly and approachable in tone, but factual and objective in substance.
- Information-dense: no filler words (e.g., "basically", "actually", "just", "really", "very"), no repetition. Every sentence earns its place.
- Make each idea clear on first reading.
- Ground explanations in specific examples and scenarios, not abstract descriptions.
- State assumptions, constraints, and uncertainty directly, rather than overstating confidence.
- Definitions before examples, with links for readers who want more depth.
- Consistent grammatical structure across list items and comparable elements.
- In definition-style lists, separate the term from its description with a colon, not an em-dash (e.g., "Term: description.", not "Term — description.").
- Active voice preferred.
- Oxford comma always.
- List items end with a full stop (or other terminal punctuation).
- Blank line before and after every list block.

## Claude-isms

Avoid these words and patterns: they mark text as Claude's rather than Gus's. The list covers Claude only, as other LLM families have different tells.

Vocabulary used figuratively. Literal senses and established terms are fine (e.g., "a load-bearing wall", "attack surface", "logic gate", "lower bound").

- Structural metaphors ("load-bearing", "spine", "seam", "grain", "shape", "layer", "scaffold", "wiring", "handoff", "surface", "routing"): name the component or dependency itself.
- Gating ("gate" as a verb, "X-gated", "hard gate", "hard stop", "hard constraint", "hard boundary"): "requires", "only if", "must".
- Movement verbs ("plumb" or "thread" through, "fold into", "reach for", "lean on"): "pass", "merge", "use", "rely on".
- Process jargon ("canonical", "drift", "parity", "probe", "landed", "verdict", "audited", "provenance", "lineage", "calibrated"): the everyday word (e.g., "merged" for "landed", "result" for "verdict").
- Research register ("frontier", "horizon", "floor", "regime", "trajectory", "slice", "headline", "exchange rate", "clears", "survives", "implicates"): the everyday word, without implying a measurement nobody took.
- Hazard metaphors ("bite", "sharp edges", "footgun", "tension"): name the failure, risk, or trade-off.
- Hollow qualifiers ("crisp", "cleanly", "principled", "genuinely", "honestly", "concretely"): say what makes it so, or drop the word.

Patterns:

- Flattering openers ("Great question!", "You're absolutely right"): start with the answer.
- Signposts and emphatic framing ("It's worth noting that", "The key insight is", "Here's the thing", "The distinction matters"): state the point.
- Contrastive reframes ("X, not Y", "not X but Y", "less X than Y", "It's not X, it's Y"): state Y, unless X is a claim someone made.
- Plain relationships named as concepts ("the ownership boundary", "the approval path"): describe the relationship.
- Coined hyphenated compounds ("owner-gated", "config-backed", "caller-first"): use a clause (e.g., "only the owner can approve it").
- Rhetorical questions answered at once ("The catch? …", "The fix? …"): state the answer.
- Mirrored clause pairs for cadence ("The client retries; the server deduplicates."): keep them only where the comparison is the point.
- Short, sharp sentences for effect ("Simple. Fast. Done.", "Nothing else touches it."): merge into the previous sentence or drop.
- Triplets for rhythm ("fast, simple, and reliable" when only speed matters): keep the items that apply.
- Closing recaps and offers ("In short, …", "Let me know if …"): end on the last substantive point.

## Nomenclature

- _Internet_ (capital I) for the global network; _internet_ (lowercase i) for a generic network of networks.
- _Web_ (capital W) for the World Wide Web.

## British English

- Proper nouns and pre-existing identifiers (`background-color`, `gray` in CSS, `center` in HTML) remain in American English. Example: software licences like "MIT License".
- Default to _-ise_ for all _-ise_/_-ize_ variants (e.g., "serialise", "normalise", "initialise", "optimise", "synchronise", "authorise", "customise", "analyse").
- Doubled consonants before suffixes: "modelling", "labelling", "cancelling", "travelling", etc.
- Key vocabulary: "behaviour", "colour", "centre", "defence", "despatch", "disc", "licence" (noun only), "grey", "fulfil", "spelt".
- Always "whilst" as a conjunction, not "while" (except where grammatically required; e.g., "once in a while").
- *Programme* for non-software contexts (training programme, conference programme); *program* for software.
- No full stop after abbreviations: "Dr", "Mr", "Mrs", "vs" (not "Dr.", "Mr.", "Mrs.", "vs.").
- Dates: DD Month YYYY (e.g., 22 February 2026). Never MM/DD/YYYY.
- Times: 24-hour format without leading zero (e.g., 9:00, 17:30).

Compliant example:

> The organisation's modelling of programme behaviour spans three centres, with results serialised at 17:30 on 22 February. Dr Smith fulfilled the licence requirements, arranged the despatch, and updated the programme schedule, whilst the defence team analysed the grey colour scheme and realised a field name had been misspelt.

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

- Contractions encouraged ("don't", "isn't", "I've", etc.).
- British colloquial constructions: "I've got X", "I haven't got X", "have you got X?".
- No em-dashes.
- Emojis sparingly — only to convey or emphasise emotions.

Compliant example:

> I've got a question about this.

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
