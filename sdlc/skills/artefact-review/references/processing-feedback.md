# Processing feedback

## Findings

Feedback can come in any format (e.g., a report, comments on a pull request, a chat message), so you MUST first break it down into individual findings, and grade any that lacks a severity.

Whoever raised a finding, you MUST judge it, and its severity, against the requirements, the conventions, and your priorities. You MUST NOT accept a finding to be agreeable, nor dispute one to spare yourself work.

You MUST respond to each finding in one of the following ways:

- Address it, if you agree with it. Where it prescribes a fix, you MAY address it differently.
- Defer it, if you agree with it, but its severity allows the artefact to ship despite it and addressing it now isn't worth the cost (e.g., fixing a pre-existing issue would widen the change).
- Dispute it, if you disagree with it, or with a severity that stops you from deferring it, giving reasons that can be checked (e.g., the requirement that it contradicts, the evidence that its consequence can't happen).

Where a finding is ambiguous, you SHOULD act on a reasonable interpretation of it, and state that interpretation in your reply.

Addressing a finding is a change like any other, so it requires confirmation wherever the /sdlc:escalation skill says so.

Where a finding that you've disputed is raised again and you still disagree, you MUST escalate the disagreement, laying out both positions, rather than dispute it again.

## Reply

Unless you're asked to use a different template or format, you MUST reply using the [reply template](../assets/reply.md), accounting for every finding, and leaving out any section that has nothing in it.
