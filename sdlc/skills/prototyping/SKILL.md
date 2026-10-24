---
name: prototyping
description: How to plan, build, and report on a throwaway prototype that de-risks a project. Planning, building, the people taking part, evidence, reporting, and risk responses. Use when planning, building, or reviewing a prototype, its plan, or its report.
---
# Prototyping

A _prototype_ is software built to answer questions about a project, and thrown away once it has answered them, even where it's built in an existing codebase. It may be built to put something tangible in front of customers or users, to establish whether the project is feasible, or to show what building it for real would entail.

A _risk_ is an uncertain event that would harm the project if it occurred (a _threat_), or benefit it (an _opportunity_).

## Plan

- The prototype MUST be planned before it's built, and the plan MUST be updated whenever a result changes its questions or its compromises.
- Every question MUST trace to a risk, and a question whose answer wouldn't change a decision MUST be dropped.
- A technical question MUST be stated as a hypothesis, along with the result that would refute it.
- Every compromise to the system architecture, security, or privacy MUST be listed in the plan, along with why the uncertainty around it is low enough to afford it.

## Build

- Effort MUST go into what the questions depend on. Whatever is already known to work MUST be left out or stubbed.
- Whatever only serves code that has to last (e.g., unit tests, documentation, continuous integration, linting, the conventions of the codebase it's built in) SHOULD be left out.
- In an existing codebase, the prototype MUST be kept apart from the code that ships, so that none of it can ship by accident.
- A path outside the main journeys MAY be left unimplemented. Where one is, it MUST fail immediately and state that the case is unsupported, so that the gap can't be mistaken for a defect.

## People taking part

- A compromise MUST NOT extend to people who aren't taking part: the prototype MUST NOT be able to overwhelm another system or be used against one, and MUST NOT collect their data or spend their devices' resources.
- A protection for those who do take part MAY be left out only where they're told before they use the prototype, and can decline.

## Evidence

- Whatever a technical hypothesis is about (e.g., a network, a provider, a device) MUST be the real thing, rather than a substitute for it.
- The prototype MUST be tested from the outside, in the environment it's meant to run in: an end-user application through what a user would do, a server-side application through what a client would do, and a library through what a consuming application would do. Units MUST NOT be tested individually.
- The tests MUST cover the main journeys and the technical hypotheses, and nothing else.
- A technical hypothesis MUST be deemed proven only once it has passed a test that could have refuted it. The test, and the result that would refute the hypothesis, MUST NOT be weakened once the test has run.
- Every result MUST be reported with the conditions under which it was obtained (e.g., the devices, the network, the load, any compromise that could have affected it).

## Report

- The prototype MUST end with a report.
- The report MUST state its conclusions, leaving out how they were reached, except for the evidence behind each answer.
- A question that the prototype couldn't answer MUST be reported as unanswered.
- Every risk that the prototype revealed, whether or not a question asked about it, MUST be listed with a recommended response.
- Once the report is written, any infrastructure that the prototype provisioned MUST be removed, along with any data that it collected. The prototype MUST NOT be deployed to production.

## Risk responses

Each risk MUST be given one of the following responses, from the [PMBOK Guide](https://www.pmi.org/standards/pmbok). A response is a recommendation about the project: any hazard that your own work introduces is still subject to the _escalation_ skill.

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

## Templates

Unless you're asked to use a different template or format, the plan and the report MUST use their templates, leaving out any section that has nothing in it.

- [Prototype plan](assets/plan.md)
- [Prototype report](assets/report.md)
