# Task Consolidation

A command-only Spec Kit preset that reviews generated tasks, removes redundant
work, and right-sizes cohesive outcomes while preserving coverage, dependencies,
and useful parallelism. Safe delivery boundaries and verifiable outcomes matter
more than reducing task count.

## Requirements

- Spec Kit `>=1.2.1` (the initial compatibility target).
- An initialized Spec Kit project with an agent integration and the design
  artifacts required by `speckit.tasks`.

Composition, installation, reinstallation, and removal have been validated with
Spec Kit `1.2.1`. Behavioral evaluation of generated task lists remains pending.

## Installation

From the root of your initialized Spec Kit project, install release `v0.2.0`:

```bash
specify preset add --from https://github.com/grafvonb/spec-kit-preset-task-consolidation/archive/refs/tags/v0.2.0.zip
```

This installs the versioned release directly; no catalog entry is required.
See the [release notes](https://github.com/grafvonb/spec-kit-preset-task-consolidation/releases/tag/v0.2.0)
for scope and validation limits.

### Local development installation

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

Spec Kit `>=1.2.3` reads [.presetignore](.presetignore) beside `preset.yml` to
exclude repository metadata, IDE settings, and temporary files from the installed
preset. These rules apply to local and archive installations; `.gitignore` does
not control installation filtering. Older CLI versions do not apply these rules.

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

The review turns fragmented or oversized work into bounded implementation steps
with exact paths and observable acceptance checks. It keeps public inputs behind
required guards, gives tests clear ownership, and separates local implementation
checks from live acceptance that needs an external environment. Common completion
rules are stated once; actual prerequisites remain distinct from scheduling choices.

Required coverage, story/phase boundaries, test-first ordering, and useful parallel
work are preserved. Task IDs are renumbered and references repaired. The report
briefly explains the main changes, or says none were needed. There is no task-count
target, extra approval step, or requirement to justify every unchanged task.

This supports focused implementation iterations, including Ralph-style execution,
but does not convert tasks to Ralph JSON or change the underlying workflow.
Consolidation follows agent instructions; it is not a deterministic formatter.

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
- [LICENSE](LICENSE): MIT license.
