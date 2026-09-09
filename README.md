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

- `architect`: Systems Architect, owning everything outside the process: the contracts between systems, the backing services and the data they hold, and the deployment topology, with security and privacy ahead of fitness for purpose, resilience, cost-effectiveness, operability, and replaceability.
- `programmer`: Programmer and Software Architect, owning the codebase, its data model, and its security and privacy guarantees, in that order of priority ahead of correctness, reliability, performance, and maintainability.

Skills:

- `programming`: How to write and review code in any language, covering code organisation, naming, data modelling, failure paths, security and privacy, and tests, with references for libraries, server-side apps, end-user apps, cryptography, and instrumentation.
- `systems-architecture`: How to design and review anything beyond the process boundary, covering trust boundaries, data and retention, threat models, failure paths, cost, operability, and replaceability, with references for server-side systems, end-user systems, contracts, cloud infrastructure, design records, and prototyping.
