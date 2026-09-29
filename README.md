# My personal Claude Code marketplace

Plugins that teach Claude Code how I work: how I write, and how I build software.

```
/plugin marketplace add gnarea/clone
```

## `ghost-writing`

Conventions for drafting and editing text on my behalf, so the output reads as mine rather than the model's.

Skills:

- `ghost-writing`: Tone, British English spelling, nomenclature, and formatting, selected by the formality of the context: informal for chat, semi-formal for docs, formal for specs.
- `issue-tracking`: Templates and rules for creating, updating, and closing issues in any tracker, including the sign-off required before writing to one.

## `sdlc`

The software development lifecycle, expressed as agents that carry a role's priorities and skills that carry its conventions.

_Endgame:_ to offload as much as I can to the LLM, so I can operate a "dark software factory" where I play the roles of Product Manager, Program Manager, Project Manager, and ultimate Systems Architect.

Agents:

- `programmer`: Programmer and Software Architect, owning the codebase, its data model, and its security and privacy guarantees, in that order of priority ahead of correctness, reliability, performance, and maintainability.

Skills:

- `programming`: How to write and review code in any language, covering code organisation, naming, data modelling, failure paths, security and privacy, and tests, with references for libraries, server-side apps, end-user apps, cryptography, and instrumentation.
