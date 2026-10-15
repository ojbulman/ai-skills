---
name: task-list-execution
description: "Use when implementing or continuing work defined by an ordered, numbered task list, checklist, or implementation plan in a Markdown file. Work through tasks and sub-items (1.1, 1.2, ...) strictly one at a time and in document order, updating progress as each is verified."
---

# Ordered Task-List Execution

Use this workflow when the user asks to carry out work recorded in a Markdown
task list, checklist, or implementation plan.

## Procedure

1. Locate and read the referenced Markdown file and enough of the relevant
   codebase to understand the first incomplete task. Treat read-only snapshots
   and attachments as reference material; do not edit them.
2. Interpret the task list's structure and order from its headings, numbering,
   and checklist sequence. Preserve that order; do not reorder, batch, or
   parallelize independent-looking items.
3. Select the first incomplete task or subtask in document order. Work only on
   that item. If it contains subtasks, complete them one by one in their listed
   order, and do not begin another top-level task until the current task and
   its subtasks are finished.
4. Implement the selected item completely, including directly related tests
   and documentation. Do not make unrelated changes.
5. Run the smallest relevant validation for the item. A task is not complete
   until its required behavior is verified; do not mark it done based only on
   implementation or an attempted test.
6. Update the source Markdown task list immediately after verification using
   its existing status convention. If it has no status convention, use
   `[ ]` for pending, `[-]` for in progress, `[x]` for verified complete, and
   `[!]` for blocked, with a brief reason for a blocked item.
7. Then proceed to the next incomplete item in document order, repeating this
   process. Continue until the user-requested scope is complete or a blocker
   requires input.
8. If an item is ambiguous, blocked, or cannot be safely completed without a
   decision, do not skip it or start a later item. Record the blocker in the
   task file where appropriate and ask the user how to proceed.
9. Preserve existing user changes. Do not mark work done if validation fails;
   report the failure, keep the item in progress or mark it blocked, and
   address it before advancing.

## Numbering and status conventions

- Every task and sub-item must be numbered hierarchically (`1`, `1.1`, `1.2`,
  `2`, `2.1`, ...), so items can be referenced unambiguously ("do 3.2").
  If the file lacks numbers, add them before starting; do not renumber
  existing numbers, and when items are removed or inserted, say so rather than
  silently renumbering.
- Reference items by number in progress updates and in the final response.
- Besides `[ ]`, `[-]`, `[x]`, `[!]`, use `[~]` for an item the user has
  deferred or marked out of scope, with a one-line reason. Reuse any
  convention the file already defines, and keep a status key in the file.

## Validation that needs the user

- When the environment cannot run the required validation (different runtime
  version, no database, no hardware), say so once, give the exact command or
  steps for the user to run, and say what output to paste back and what
  result you expect.
- Keep the item `[-]` until output confirms it. Compare the output with the
  expected result explicitly; do not assume success. If the result shows the
  change was never exercised (for example the new code did not appear in the
  log), report that and fix the cause before continuing.
- Say which sub-claims are verified and which are still untested; a config or
  syntax check alone does not verify behaviour.

## Decisions and scope changes

- Use the ask-user tool for design choices, one question at a time, and record
  the answer under the file's decisions/notes section.
- When the user removes, defers, or moves items or the file itself, update
  the task list immediately and do not resurrect the items. Preserve blank
  lines and headings when deleting lines, and re-read the edited range.
- Edit status markers with a targeted edit and confirm the line number first;
  line-number based edits are fragile once lines are added or removed.
- Keep task files out of version control when they live in an ignored folder,
  and do not mention untracked helper files as deliverables.

## Progress and response

- Keep the task file as the source of truth for progress; do not create a
  separate tracking document unless requested.
- Do not claim later tasks are complete when only an earlier task was handled.
- Begin each update with the item number being worked on and its new status.
- When a task finishes, state any follow-up risks that are outside the list
  (for example deployment prerequisites) in one or two lines.
- In the final response, summarize completed task items, their validation, and
  any remaining or blocked items.
