# M1.2: Process IR Machine-Readiness Hardening

- Milestone ID: `M1.2`
- Title: Process IR Machine-Readiness Hardening
- Status: Proposed
- Implementation status: In progress

## Objective

Convert the accepted M1 semantic contract into a machine-ready contract design without implementing runtime components.

## Scope

- Common `RecordEnvelope`.
- Immutable record and revision semantics.
- Effective-status derivation.
- Deterministic Semantic Compiler replay contract.
- Version and digest metadata.
- Diagnostic severity and blocking model.
- Diagnostic aggregation.
- AnalystDecision staleness and invalidation.
- Mapping-rule references and versioning.
- Exact target BPMN profile identity, compatibility, and propagation design.
- Detailed partial-compilation dependency-closure policy.
- Expanded contract-test matrix.

## Explicit non-goals

- No machine-readable schema.
- No parser, compiler, BPMN Kernel, runtime agent, UI, persistence, or transport implementation.
- No executable validation rules or tests.
- No confidential source material.

## Deliverables

- Proposed design outcomes tracked by Issues [#16](https://github.com/ThresholdOps/MotiveForce/issues/16)-[#21](https://github.com/ThresholdOps/MotiveForce/issues/21).
- Project-memory updates recording accepted M1.2 decisions when they are made.

## Acceptance basis

M1.2 is not completed. M1 semantic acceptance is satisfied by merged PR #2. M1.2.1 through M1.2.4 are accepted and completed as design-contract work through PRs #22 through #25. M1.2.5 is accepted and approved for completion as design-contract work through merge of PR #26. Issue #8 and Issue #21 remain deferred, so M1.2 as a whole remains incomplete.

## Related PRs

- Merged [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2) defines the accepted M1 semantic contract.
- [PR #3](https://github.com/ThresholdOps/MotiveForce/pull/3) registers this milestone record.
- [PR #22](https://github.com/ThresholdOps/MotiveForce/pull/22) completes M1.2.1 design-contract work.
- [PR #23](https://github.com/ThresholdOps/MotiveForce/pull/23) completes the accepted M1.2.2 deterministic replay design through merge.
- [PR #24](https://github.com/ThresholdOps/MotiveForce/pull/24), from branch `design/m1-2-3-diagnostic-policy`, completes the accepted diagnostic severity and aggregation design through merge.
- [PR #25](https://github.com/ThresholdOps/MotiveForce/pull/25), from branch `design/m1-2-4-analyst-decision-staleness`, completes the accepted M1.2.4 design through merge.
- M1.2.5 is accepted and approved for completion as design-contract work through merge of [PR #26](https://github.com/ThresholdOps/MotiveForce/pull/26) from branch `design/m1-2-5-mapping-profile-propagation`.
- [REV-0011](../reviews/M1-2-5-mapping-rule-target-profile-propagation-review.md) and [REV-0012](../reviews/M1-2-5-mapping-rule-target-profile-propagation-review-2.md) recorded Request changes. Final human review [REV-0013](../reviews/M1-2-5-mapping-rule-target-profile-propagation-review-3.md) approves frozen semantic head [`f8d2249e4693305b57bf021c76bdd78b010da24b`](https://github.com/ThresholdOps/MotiveForce/commit/f8d2249e4693305b57bf021c76bdd78b010da24b), closes both REV-0012 findings, and authorizes bounded finalization and merge without authorizing implementation.

## Related commits

- M1 final source head [`b2d6fe8f2192149145e04cbf2f0e5ffea737e1c0`](https://github.com/ThresholdOps/MotiveForce/commit/b2d6fe8f2192149145e04cbf2f0e5ffea737e1c0)
- M1 merge commit [`54d5e814601788574d13761561867ce5982cc88c`](https://github.com/ThresholdOps/MotiveForce/commit/54d5e814601788574d13761561867ce5982cc88c)
- M1.2.1 final source head [`c969aa842ad4c4565eb7fcafd51b54d32c3520f4`](https://github.com/ThresholdOps/MotiveForce/commit/c969aa842ad4c4565eb7fcafd51b54d32c3520f4)
- M1.2.1 squash merge commit [`034cdcd4c680d23bcd68b8ad959d0c4163532d9c`](https://github.com/ThresholdOps/MotiveForce/commit/034cdcd4c680d23bcd68b8ad959d0c4163532d9c)
- M1.2.2 squash merge commit [`a63858354f6e34f7b56900dd5a89d04ac0b19cb5`](https://github.com/ThresholdOps/MotiveForce/commit/a63858354f6e34f7b56900dd5a89d04ac0b19cb5)
- M1.2.3 squash merge commit [`006574b25732f0776a7e510fd33838c9946d9677`](https://github.com/ThresholdOps/MotiveForce/commit/006574b25732f0776a7e510fd33838c9946d9677)
- M1.2.4 squash merge commit [`20f53f13938692b9c572b6f9f963e89fc22cb5b8`](https://github.com/ThresholdOps/MotiveForce/commit/20f53f13938692b9c572b6f9f963e89fc22cb5b8)

## Decisions created

- [DEC-0005](../decisions/DEC-0005-record-envelope-revision-semantics.md), Accepted.
- [DEC-0006](../decisions/DEC-0006-deterministic-semantic-compiler-replay.md), Accepted through merge of PR #23.
- [DEC-0007](../decisions/DEC-0007-process-ir-diagnostic-severity-aggregation.md), Accepted through merge of PR #24.
- [DEC-0008](../decisions/DEC-0008-analyst-decision-staleness-revalidation.md), Accepted through merge of PR #25.
- [DEC-0009](../decisions/DEC-0009-mapping-rule-target-profile-propagation.md), Accepted through merge of PR #26.

## Outcome

Proposed and in progress at the design-program level. M1.2.1 through M1.2.4 design-contract work are completed, and M1.2.5 is accepted and approved for completion through merge of PR #26. M1.2 as a whole is not completed because Issue #8 and Issue #21 remain deferred. No runtime implementation has started.

## Follow-up

- [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16): record envelope and revision semantics, completed as M1.2.1 design work.
- [Issue #17](https://github.com/ThresholdOps/MotiveForce/issues/17): deterministic compiler replay contract, completed through merge of PR #23.
- [Issue #18](https://github.com/ThresholdOps/MotiveForce/issues/18): diagnostic severity and aggregation, completed as M1.2.3 design-contract work through merge of PR #24.
- [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19): AnalystDecision staleness, invalidation, revalidation, and controlled authority carry-forward, completed as M1.2.4 design work through merge of PR #25.
- [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20): mapping-rule references, ruleset versioning, and target-profile propagation, approved as completed M1.2.5 design work through merge of PR #26; close after merge.
- [Issue #21](https://github.com/ThresholdOps/MotiveForce/issues/21): expanded Process IR contract test matrix.
- [Issue #8](https://github.com/ThresholdOps/MotiveForce/issues/8): detailed partial-compilation dependency policy retained from earlier open-item registration.
