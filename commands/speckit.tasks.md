## Task Consolidation: Execution Order

Read this entire command before executing it. Follow the underlying task-generation
workflow below, with one additional mandatory review: after drafting `tasks.md`,
perform the Task Consolidation Review defined below and save the consolidated
artifact **before entering Mandatory Post-Execution Hooks or the Completion
Report**. Treat this review as the final part of task generation, not as work to
perform after the underlying command finishes.

Preserve the underlying setup, input handling, task template, pre-execution checks,
hook behavior, handoffs, and completion requirements. Post-execution hooks must
receive the consolidated `tasks.md`; run them in their normal position after the
review. Do not report completion until both the review and the required hook
handling are complete.

{CORE_TEMPLATE}

## Task Consolidation Review

Execute this section at the insertion point specified above. Its placement here
does not change the execution order.

1. **Check the draft against its sources.** Review the drafted tasks against the
   specification, plan, available design documents, user instructions, and
   applicable constitution. Identify the requirements, acceptance criteria,
   prerequisites, and requested verification that each task serves. Judge work by
   its contribution to those sources, not by task count.

2. **Remove unnecessary work.** Remove duplicate tasks, redundant setup, and work
   unsupported by the feature or project requirements. If a task duplicates part
   of another task, retain its necessary scope in the surviving task. Do not drop
   required behavior, error handling, security, accessibility, documentation, or
   verification merely to shorten the list. If the need for a task is uncertain,
   retain it rather than silently reducing coverage.

3. **Merge overly granular steps.** Combine closely related steps when they form
   one cohesive, clearly bounded implementation outcome in the same story and
   phase. Preserve exact file paths, acceptance-relevant details, and any required
   internal ordering in the merged description. Keep tasks separate when they
   represent independently verifiable outcomes, meaningful dependency boundaries,
   or useful parallel work. Do not combine unrelated work into broad tasks such
   as "implement the feature," merge across user stories, or absorb foundational
   prerequisites into downstream story tasks.

4. **Preserve the workflow's guarantees.** Keep story priorities, phase structure,
   independent story testability, and MVP-first incremental delivery. Preserve
   explicitly requested tests and their required ordering; do not merge tests
   into implementation tasks if that would hide a required test-first step. Follow
   the underlying command's rules for when tests are generated. Do not invent
   additional scope or testing requirements as part of consolidation.

5. **Repair the task list and supporting sections.** Assign unique, sequential
   task IDs in execution order and update all affected references in `tasks.md`.
   Preserve the required checkbox syntax, story labels, and actionable
   descriptions with exact file paths. Re-evaluate every `[P]` marker after
   merging: retain it only when the resulting task has no dependency on incomplete
   tasks and does not conflict with the files of concurrently scheduled work.
   Update dependencies, story ordering, parallel execution examples, and the
   implementation strategy to match the surviving tasks. Ensure there are no
   dangling references, dependency cycles, or stale task counts.

6. **Validate and save before hooks.** Recheck coverage against the sources and
   confirm that each surviving task is specific enough to execute without
   reconstructing the removed tasks. Save the final consolidated `tasks.md` using
   the underlying template's structure. There is no fixed task-count limit,
   reduction quota, or preferred reduction percentage. Leave an already
   appropriately sized task list unchanged. Then resume the underlying mandatory
   post-execution hook handling and completion report.

## Completion Report Addition

Include a concise consolidation summary in the underlying Completion Report:

- Draft and consolidated task counts, with the required final per-story counts
  and parallel opportunities reflecting the consolidated artifact.
- Significant removals or merges and why they preserve required coverage; use
  final task IDs when referring to surviving tasks.
- If no changes were warranted, state that the review retained the draft as-is.

Keep this explanation in the completion report rather than adding bookkeeping
tasks or unrelated sections to `tasks.md`. The command is done only when the
consolidation review and all underlying completion requirements are satisfied.
