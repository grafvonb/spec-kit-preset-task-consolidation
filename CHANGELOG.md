# Changelog

## 0.1.0 — Unreleased

### Added

- Command-only `task-consolidation` preset targeting Spec Kit `>=1.2.1`.
- A `speckit.tasks` wrapper that reviews and consolidates drafted tasks before
  post-execution hooks and the completion report.
- Instructions to preserve requirement coverage, story boundaries, requested
  tests, dependencies, and useful parallelism without imposing a task-count target.
- Task ID and reference repair, refreshed supporting sections, and a completion
  summary explaining significant consolidation changes.
- Documentation for local installation, usage, inspection, reinstallation, and removal.

### Changed

- Review task boundaries for behavioral safety, contract consistency, verification
  ownership, external dependencies, and practical size; allow justified splits.
- Separate functional dependencies from scheduling, share common completion rules,
  and distinguish fixture implementation from pending live acceptance.
- Preserve sequential ID repair, test-first ordering, source traceability, and hook
  behavior; report material boundary decisions without an extra approval gate.
- Keep the review implementation-focused, with brief reporting and no per-boundary
  assessment paperwork.
- Add synthetic behavioral regression cases with explicit expectations and pending
  execution status.
