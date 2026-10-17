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

Review against the specification, plan, repository instructions, and constitution.
Preserve required scope, traceability, story/phase boundaries, and the underlying
rules for generating tests and test-first ordering. Resolve instruction conflicts
by precedence and explain material conflicts. Do not add an approval step.

1. **Make each task a bounded implementation step.** Remove duplicate or
   unsupported work; retain it if its necessity is uncertain. Merge related steps
   in the same story and phase when they deliver one outcome. Keep interface,
   implementation, and test-double changes together if separation breaks the
   contract or build. Split oversized work at independently verifiable outcomes.
   Each task should fit a focused implementation iteration and state its outcome,
   exact paths, unique constraints, and observable acceptance checks. Keep required
   behavior-specific tests and documentation with their implementation scope,
   preserving separate test-first steps where required.

2. **Keep intermediate behavior safe.** Do not expose public inputs before their
   validation and compatibility guards exist. Include enablement with the guards
   or defer it until they are ready. If several tasks form one delivery unit, state
   their required order and delivery checkpoint. Task boundaries need not be release
   boundaries; expected failing test-first steps are valid. Do not call an
   incomplete or unverified sequence a deliverable MVP.

3. **Make verification actionable.** Identify which task adds each required test,
   which existing regression tests to rerun, and what distinct behavior any
   overlapping test layers prove. Avoid duplicate test implementation. Separate
   locally verifiable test/fixture work from live acceptance when infrastructure,
   credentials, or server versions are required. State those prerequisites and the
   expected result; unavailable or skipped validation stays pending, never passing.
   Do not invent new testing requirements.

4. **Keep ordering and instructions lean.** Distinguish actual prerequisites from
   preferred execution order. Shared files may prevent parallel work without
   creating a functional dependency. Preserve mandatory workflow ordering. State
   common formatting, documentation policy, progress tracking, and validation rules
   once in an existing template section or reference their source; keep task-specific
   details in the task. Do not add review matrices or bookkeeping tasks.

5. **Repair and save.** Check coverage and whether the resulting tasks can be
   executed without reconstructing removed details. Preserve checklist syntax and
   story labels; renumber IDs sequentially and repair references. Update dependencies,
   counts, parallel examples, and delivery strategy; check for dangling references
   and cycles. Retain `[P]` only with no incomplete prerequisites or concurrent file
   conflicts. Save before post-execution hooks, then resume the underlying workflow.

Use concrete behavior, contracts, acceptance checks, external prerequisites, and
iteration size to justify changes. There is no task-count target: more, fewer, or
unchanged tasks may be appropriate. Do not justify every unchanged boundary.

## Completion Report Addition

Add a brief summary to the underlying report: draft → final task count and the
main changes with their reasons (using final IDs), or state that no changes were
needed. Mention unresolved constraints or pending external validation when relevant.
Keep required final per-story counts and parallel opportunities accurate. Reviewing
tasks does not execute their acceptance checks.
