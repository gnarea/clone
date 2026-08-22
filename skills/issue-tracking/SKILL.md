---
name: issue-tracking
description: How Gus wants issues and tasks managed in any issue tracker (GitHub, Jira, Linear, etc.). Apply when creating, refining, updating or closing issues on his behalf.
user-invocable: false
---

Applies to any issue tracker. Translate the vocabulary below into whatever the tracker uses: an _issue_ may be a ticket, a task, a story, or a work item.

Every issue you write or edit MUST observe the [ghost-writing](../ghost-writing/SKILL.md) skill: semi-formal for titles and descriptions, informal for comments.

## Before Creating an Issue

1. Search the tracker for an existing report, covering both open and closed issues, and searching by symptom as well as by suspected cause. For example, a report of "the export button does nothing" may already exist as "CSV export fails silently for empty projects".
2. If a match exists, add the new information as a comment there instead of opening a duplicate.
3. If the match is closed and the problem has returned, comment on it and ask whether to reopen it or file a follow-up.

## Writing the Issue

Frame the issue in terms of the product and the user experience. Describe what a person tries to do, what happens instead, and what should happen. Reserve technical framing for issues that are inherently technical, such as a dependency upgrade or a refactor with no user-visible surface.

Structure:

- Title: the problem or the outcome, in one line.
- Context: who is affected and in which scenario.
- Current behaviour: what happens today, with the steps that reproduce it.
- Desired behaviour: what should happen instead, and how to tell when it is done.
- Implementation pointers: high-level notes on where the work will land, at the end of the document, only if such details are already known.

Keep implementation pointers as pointers. Name the components, files, or endpoints involved and the constraints that will shape the fix. Leave the design to the implementer.

Be succinct. Cut anything a reader does not need in order to act. Prefer a link to a log, a screenshot, or a prior discussion over a transcript pasted inline.

Compliant example:

> **Title:** Exporting a project with no tasks produces an empty file
>
> **Context:** Users who create a project and export it before adding any tasks.
>
> **Current behaviour:** The export downloads a 0-byte CSV file with no headers or warning, so users assume their tasks were lost.
>
> **Desired behaviour:** The export contains the column headers, and the app tells the user that the project has no tasks yet.
>
> **Implementation pointers:** The CSV writer in `exporters/csv.py` returns early when the task list is empty.

## Updating an Issue

- Keep the description as the current source of truth: edit it when the understanding of the problem changes, rather than appending corrections.
- Record discussion, findings, and decisions in comments, and fold the conclusions back into the description.
- State explicitly when the scope changes, so that subscribers can see what moved.
- Split the issue in two when it grows a second, separable outcome, and link the parts to each other.

## Closing an Issue

- Say what changed and how it was verified, linking to the change that resolved it.
- Close as "not planned", or the tracker's equivalent, when the issue will not be acted upon, and give the reason.
