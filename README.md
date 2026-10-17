# Task Consolidation

A command-only Spec Kit preset that reviews generated tasks, removes redundant
work, and merges overly granular steps while preserving coverage, dependencies,
and useful parallelism.

## Requirements

- Spec Kit `>=1.2.1` (the initial compatibility target).
- An initialized Spec Kit project with an agent integration and the design
  artifacts required by `speckit.tasks`.

Composition, installation, reinstallation, and removal have been validated with
Spec Kit `1.2.1`. Behavioral evaluation of generated task lists remains pending.

## Installation

Clone this repository:

```bash
git clone https://github.com/grafvonb/spec-kit-preset-task-consolidation.git
```

From the root of your initialized Spec Kit project, install the local preset.
Replace the example path with the absolute path to your clone:

```bash
specify preset add --dev /absolute/path/to/spec-kit-preset-task-consolidation
```

This is a local development installation. A published release or catalog entry
is not required.

## Usage and behavior

Run `speckit.tasks` through your agent's normal command or skill invocation. No
separate consolidation command is needed. Installing the preset does not itself
rewrite an existing `tasks.md`.

The preset provides one command override, `speckit.tasks`, using the `wrap`
strategy and `{CORE_TEMPLATE}` to retain the underlying command. It adds no
extension, runtime scripts, or artifact-template overrides.

The command follows this execution order:

1. Run the underlying setup, pre-execution checks, and task-generation workflow.
2. Review and consolidate the drafted `tasks.md`, then save it.
3. Handle the underlying post-execution hooks against the consolidated artifact.
4. Report completion, including a concise consolidation summary.

During the review, the agent is instructed to:

- Remove duplicates, redundant setup, and work unsupported by the feature or
  project requirements; retain tasks when their necessity is uncertain.
- Merge related small steps only when they form a cohesive outcome in the same
  story and phase, with enough detail and exact file paths to remain actionable.
- Preserve requirements, acceptance criteria, story boundaries, prerequisites,
  independent story testability, and useful parallel work.
- Preserve requested tests and required test-first ordering, following the
  underlying command's rules for when tests are generated.
- Renumber tasks and repair references, dependencies, `[P]` markers, counts,
  parallel execution examples, and implementation strategy.

There is no fixed task-count limit, reduction quota, or target percentage. An
appropriately sized task list should remain unchanged. The completion report
includes draft and consolidated counts and explains significant removals or
merges, or states that no changes were warranted.

Use this preset when task generation produces redundant work or fragments a
cohesive change into unnecessarily small steps. It is not intended to enforce a
fixed planning budget, combine unrelated work, or remove required coverage to
make a task list shorter. Consolidation is performed by the agent following the
prompt; it is not a deterministic task-list formatter.

## Inspect the installation

From the target project's root, run:

```bash
specify preset resolve speckit.tasks
specify preset info task-consolidation
specify preset list
```

Also inspect the generated command or skill in your agent integration's directory.
Confirm that it contains the consolidation instructions and the underlying task
workflow, with no unresolved `{CORE_TEMPLATE}` placeholder. The location and file
format depend on the integration.

Other presets and project-local overrides can affect command resolution. Inspect
the effective installed command when combining this preset with other overrides.

## Updating the local preset

Commands are materialized during installation. Editing this repository does not
automatically update commands already installed in another project. Reinstall
after changing the source; from the target project's root:

```bash
specify preset remove task-consolidation
specify preset add --dev /absolute/path/to/spec-kit-preset-task-consolidation
```

Inspect the generated command again after reinstalling.

## Removal

From the target project's root:

```bash
specify preset remove task-consolidation
```

Inspect the resolved and generated command afterward to confirm the appropriate
underlying command is active. Disabling a preset alone does not remove previously
registered commands; use removal when uninstalling it.

## Validation

Lifecycle checks passed on 2026-10-17 in disposable projects initialized with the
installed Spec Kit `1.2.1` CLI and its bundled release assets:

| Integration | Generated format | Install, reinstall, removal |
| --- | --- | --- |
| Codex (`--skills`) | `SKILL.md` | Passed |
| Kilo Code | Markdown command | Passed |
| Gemini | TOML command | Passed |

Checks confirmed that command resolution composes the preset over the bundled
core command, includes the underlying workflow once, resolves the core and setup
script placeholders, and preserves the generated core command body. Reinstallation
from an edited disposable preset copy materialized the changed content. Removal
returned resolution to the bundled core and restored its command body and original
metadata values.

Restored files are not necessarily byte-for-byte identical to freshly initialized
files: Spec Kit may normalize YAML, add a skill title or source comment, and retain
script metadata. These rendering differences were inspected during validation.

These checks validate installation and composition, not agent execution. Small
and large feature trials, consolidation quality, and actual hook execution still
need behavioral evaluation.

## Project files

- [preset.yml](preset.yml): metadata, compatibility requirement, and command declaration.
- [commands/speckit.tasks.md](commands/speckit.tasks.md): consolidation wrapper.
- [CHANGELOG.md](CHANGELOG.md): version history.
- [LICENSE](LICENSE): MIT license.
