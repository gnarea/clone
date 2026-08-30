# Endgame

To offload as much as I can to the LLM, so I can operate a "dark software factory" where I play the roles of Product Manager, Program Manager, Project Manager, and ultimate Systems Architect.

## Structure/template of every agent

An agent is a job description: the priorities it optimises for, and the principles by which it delivers on them. Anything prescriptive (conventions, workflows, templates, checklists) belongs in a skill.

```markdown
---
name: <slug>
description: <Role Title>. Use to <primary deliverables>; or to review <artefacts>.
skills:
  - <skill relevant to every task this role performs>
---
# <Role Title>

(Responsibilities.)

## Priorities

(Ordered: earlier beats later when they conflict.)

## Principles

(How to deliver on the priorities, in broad terms.)

## Escalation

(When and how to escalate issues to the user or parent agent.)
```
