# Behavioral review regression cases

Status: manual evaluation specification; agent execution has not been evaluated.
These are synthetic cases, not facts about the originating project. Paths and the
version threshold below are illustrative and must not be copied into real tasks
without support from that project's sources.

## Evaluation procedure

In a disposable project, supply the stated source requirements and draft to the
consolidation review. Inspect the final tasks and completion report against the
checks below. Record the effective command/version, input, output, and pass/fail
observations. Do not treat matching instruction text as a behavioral pass. Accept
alternative task groupings that satisfy the properties; there is no target count.
Lifecycle composition and actual hook execution require their own checks.

## Suspended process instances

### Source requirements

US1 adds the public CLI filter `--state suspended` for process instances. Servers
at or above synthetic version 2.0 support it; older servers must receive no
suspended-state request and the CLI must explain that the filter is unsupported.
Existing `active` filtering must remain unchanged. Invalid state values must still
be rejected. Public parsing/dispatch must not expose the new option before its
guard exists.

The plan requires updating `Client.list_instances` in `src/client.py`, its
implementation in `src/http_client.py`, and the implementing fake in
`tests/fakes/client.py` consistently. Tests are explicitly requested, with tests
written first. Behavior documentation belongs in `docs/instances.md`. The live
suite needs credentials and both supported and older server environments, which
are unavailable during local development. Fixture setup can be checked offline.
Common rules require formatting, progress updates, and accurate validation status.

### Problematic draft: US1 phase excerpt

- [ ] T010 [US1] Write suspended-filter tests in tests/test_states.py
- [ ] T011 [US1] Accept suspended in src/cli/states.py; format and update progress
- [ ] T012 [US1] Change Client.list_instances in src/client.py
- [ ] T013 [US1] Update src/http_client.py for suspended requests
- [ ] T014 [US1] Update tests/fakes/client.py to match the client interface
- [ ] T015 [US1] Add old-server guard in src/cli/instances.py; add suspended-filter tests in tests/test_instances.py; format and update progress
- [ ] T016 [US1] Add suspended-filter tests and fixtures in tests/integration/test_instances.py and tests/integration/fixtures.py; run against live servers; mark complete if servers are unavailable
- [ ] T017 [US1] Document filter compatibility in docs/instances.md; format and update progress

The draft calls T011 an independently deliverable MVP, declares T015 dependent
on T017 solely because one developer prefers documentation first, and repeats
"test suspended filtering" without assigning distinct proof to each test layer.

### Expected result

Accept any grouping that satisfies these checks; no particular task count is
required.

- Enable `suspended` only with the old-server guard ready. Remove the premature
  MVP claim and identify the actual delivery checkpoint.
- Keep client interface, HTTP implementation, and fake consistent. Retain required
  tests-first steps without treating their expected failures as deployable states.
- Give tests distinct ownership: parser syntax, old-server rejection without an
  outgoing request, supported request serialization, and actual live behavior.
  List existing active-filter regression tests as reruns, not new implementation.
- Give fixture implementation local acceptance checks, such as collection and fake
  lifecycle checks. Keep live acceptance pending until both server environments
  and credentials are available. A skipped check cannot satisfy acceptance.
- Keep compatibility documentation in US1's scope. Remove its invented functional
  dependency on the guard; retain any real workflow ordering.
- State common completion rules once. Preserve paths, coverage, story labels, and
  traceability; repair sequential IDs, references, counts, and parallel markers.
- Briefly explain the main changes and pending validation without claiming any
  implementation or test execution occurred during the review.

## Additional boundary checks

| Input variation | Expected review result |
| --- | --- |
| One large US1 task combines guarded filtering, offline fixture construction, and credential-dependent live acceptance | Split independently verifiable outcomes where useful; retain the guarded unit and all coverage. Do not wait for live credentials to declare locally verified fixture implementation complete. |
| Two independent changes touch the same file | Record a scheduling conflict and remove unsafe parallel markers; do not invent a functional prerequisite. |
| A guard belongs to a mandated foundational phase, while enablement belongs to US1 | Retain the phase boundary and actual dependency; do not absorb foundational work into US1 just to reduce count. |
| Repository instructions require tests first, while a proposed merge would hide that step | Retain explicit tests-first ordering and explain the resolved conflict. |
| No new tests are requested or required by applicable sources | Do not invent new test tasks from this regression example; preserve applicable verification requirements. |
| Draft already has bounded safe outcomes, clear ownership, and accurate dependencies | Retain it unchanged and say why; do not merge or split to meet a quota. |
| A fixture check is skipped due to an unavailable prerequisite | Report it as unverified, not passing or completed on the strength of the skip. |

For all cases, preserve the core workflow and save before post-execution hooks.
Do not add approval gates, review matrices, or bookkeeping tasks.
