---
name: prototyping
description: How to plan, build, and report on a throwaway prototype that de-risks a project. Planning, building, the people taking part, evidence, reporting, and risk responses. Use when planning, building, or reviewing a prototype, its plan, or its report.
---
# Prototyping

A _prototype_ is software built to answer questions about a project, and thrown away once it has answered them, even where it's built in an existing codebase. It may be built to put something tangible in front of customers or users, to establish whether the project is feasible, or to show what building it for real would entail.

A _risk_ is an uncertain event that would harm the project if it occurred (a _threat_), or benefit it (an _opportunity_).

You MUST follow the guidelines for the task at hand:

- [Planning](references/planning.md) a prototype, using the [plan template](assets/plan.md).
- [Building](references/building.md) a prototype.
- [Reporting](references/reporting.md) on a prototype, using the [report template](assets/report.md).

Unless you're asked to use a different template or format, you MUST use the task's template, leaving out any section that has nothing in it.

## Lifecycle

- The prototype MUST be planned before it's designed or built, and the plan MUST be updated whenever a result changes its questions or its compromises.
- The prototype MUST end with a report. Once the report is written, any infrastructure that the prototype provisioned MUST be removed, along with any data that it collected.
- The prototype MUST NOT be deployed to production.

## People taking part

- A compromise MUST NOT extend to people who aren't taking part: the prototype MUST NOT be able to overwhelm another system or be used against one, and MUST NOT collect their data or spend their devices' resources.
- A protection for those who do take part MAY be left out only where they're told before they use the prototype, and can decline.

## Evidence

- Whatever a technical hypothesis is about (e.g., a network, a provider, a device) MUST be the real thing, rather than a substitute for it.
- A technical hypothesis MUST be deemed proven only once it has passed a test that could have refuted it. The test, and the result that would refute the hypothesis, MUST NOT be weakened once the test has run.

## Risk responses

Each risk MUST be given one of the following responses, from the [PMBOK Guide](https://www.pmi.org/standards/pmbok). A response is a recommendation about the project: any hazard that your own work introduces is still subject to the `escalation` skill.

For a threat:

- Avoid: change the plan to remove the threat or its cause (e.g., drop the feature that depends on an unproven library).
- Mitigate: reduce the threat's likelihood or impact (e.g., add a fallback for when a provider is unavailable).
- Transfer: shift the threat, and responsibility for its impact, to a third party (e.g., through insurance, or a provider's service level agreement).
- Accept: take no action, other than setting aside time or money in case the threat occurs.
- Escalate: hand the threat to whoever owns it outside the project, because responding to it is beyond the project's remit or authority (e.g., it affects another product). Responding to it is then up to them.

For an opportunity:

- Exploit: change the plan to make sure that the opportunity is realised (e.g., build on a library that removes a third of the work).
- Enhance: increase the opportunity's likelihood or impact.
- Share: give the opportunity to a third party better placed to realise it, in exchange for part of the benefit (e.g., through a partnership).
- Accept: take advantage of the opportunity if it arises, without pursuing it.
- Escalate: as for a threat.
