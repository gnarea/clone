(Keep the spec as short as the change allows: a bug fix within one component fits on a page. Make each point once, in the section it belongs to, and leave out any section that the change gives nothing to say in, rather than saying so.)

# Summary

(The problem, the proposed solution, and any consequence of the solution that must be called out. For a reader who knows the domain's vocabulary, but who may not be technical.)

# Problem

(With no solution in it, and no account of how it was found. Where a requirement is questioned, say why it was believed to be necessary, and what was wrong with it on its own terms. Use a diagram only where the problem is hard to explain without one.)

# Non-goals

(What the change deliberately won't do, even though a reader might reasonably expect it to. A decision made under the proposed solution isn't restated here.)

# Proposed solution

(What the change adds, alters, or removes, and why this over any alternative to the change as a whole. Where a diagram would convey the change faster than prose, use one.)

(Structure the rest around the decisions that the change makes, with a heading per decision unless there's only one. What needs specifying depends on what the change touches: e.g., components, exchanges, endpoints, stores, failure modes, dependencies, configuration, observability, deployment. Stay at the level of the system, leaving functions, constants, source files, and algorithms to the software architecture and the code.)

## (Decision, as a statement of what's chosen)

(Whatever it specifies, in enough detail for another architect to assess it. Where it gives up something a reviewer could contest: what it optimises for, at the expense of what, and its second-order consequences. The alternatives that a reviewer could be expected to propose, and why each was rejected. Any open question that blocks it.)

(A decision that follows from this one nests under it. An element that several decisions shape is specified once, and referred to from the others. A message format is declared in the notation closest to its wire format, marking what's added, altered, or removed. Where the change would otherwise contradict the architecture document, amending it is a decision of its own, stated as what changes and why, rather than drafted in full.)

# Impact on stakeholders

(Who the change leaves worse off, and how.)

## Limitations

(Who bears each one, and the workaround, if there is one.)

## Ethical costs

(Who bears each one, including people who aren't users, and the environment.)

## Residual risks

(What remains after the change, including what would defeat each mitigation, at what cost to the attacker, and who bears the risk. Name each attack vector in the threat model that the change affects, rather than drafting its new wording.)

# Outcome

(Once it's settled: the argument that settled it, including where the argument is that nothing was found to justify a change.)
