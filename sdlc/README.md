# Endgame

To offload as much as I can to the LLM, so I can operate a "dark software factory" where I play the roles of Product Manager, Program Manager, Project Manager, and ultimate Systems Architect.

## Structure/template of every agent

An agent is a job description: the priorities it optimises for, and the principles by which it delivers on them. Anything prescriptive (conventions, workflows, templates, checklists) belongs in a skill.

```markdown
---
name: <slug>
description: <Role Title>. Use to <primary deliverables>; or to review <artefacts>.
skills:
  - <skill that is relevant to every task this role performs>
---
# <Role Title>

<One-sentence prime directive.>

## Priorities

<Ordered: earlier beats later when they conflict.>

## Principles

<How to deliver on the priorities, in broad terms.>

## Escalation

- <Trigger>: consult the <role> agent.
- <Trigger>: stop and escalate to the user.
```

Section by section:

- `description`: the only part loaded before dispatch, so it carries the whole routing burden. Descriptions must be mutually exclusive, or the dispatcher will dither between overlapping roles.
- `skills`: skills to preload into the agent's context. Names match the skill's directory name, or `plugin:skill` when qualified. Reserve this for skills relevant to every task the role performs; anything narrower should be left to load on demand.
- Prime directive: the single thing to maximise, stated up front so it frames everything below it.
- Priorities: the ordering is the point. It is what the agent cannot infer, and what determines its behaviour when goals conflict.
- Principles: dispositions, not rules. If a principle needs examples, exceptions, or a checklist to be actionable, it is a skill.
- Escalation: peer roles to consult, plus the triggers that stop work altogether. Every chain terminates with me, which is the "dark software factory" made operational. Boundaries between adjacent roles (programmer and architect, say) are written once, as a matching pair of triggers in both agents.

Target 80 lines per agent. Breaching it usually means something in the body is a skill.

## Agent or skill?

The agent body becomes the subagent's system prompt, so it is paid for on every task that agent ever takes on. A skill body is paid for only when it is loaded. That gives the division of labour:

- Agent: what governs judgement, and applies to every task the role performs.
- Skill: what governs the form of a deliverable, or applies to only some tasks.

Two agents that would rank the same priorities in the same order are one agent with two skills. An agent whose body amounts to "apply skill X" has not earned its existence.

What to strive for whilst producing or reviewing a given deliverable belongs in that deliverable's skill, alongside the conventions themselves. Preloading keeps this available where it is needed on every task, without the agent absorbing it.
