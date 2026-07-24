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
- Target BPMN profile registry design.
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

M1.2 is not completed. M1 semantic acceptance is satisfied by merged PR #2. M1.2.1 is accepted and completed as design-contract work through [PR #22](https://github.com/ThresholdOps/MotiveForce/pull/22). M1.2.2 is accepted and completed as design-contract work through merge of [PR #23](https://github.com/ThresholdOps/MotiveForce/pull/23). Other M1.2 Issues remain deferred, and no next item is started by this delivery.

## Related PRs

- Merged [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2) defines the accepted M1 semantic contract.
- [PR #3](https://github.com/ThresholdOps/MotiveForce/pull/3) registers this milestone record.
- [PR #22](https://github.com/ThresholdOps/MotiveForce/pull/22) completes M1.2.1 design-contract work.
- [PR #23](https://github.com/ThresholdOps/MotiveForce/pull/23) completes the accepted M1.2.2 deterministic replay design through merge.

## Related commits

- M1 final source head [`b2d6fe8f2192149145e04cbf2f0e5ffea737e1c0`](https://github.com/ThresholdOps/MotiveForce/commit/b2d6fe8f2192149145e04cbf2f0e5ffea737e1c0)
- M1 merge commit [`54d5e814601788574d13761561867ce5982cc88c`](https://github.com/ThresholdOps/MotiveForce/commit/54d5e814601788574d13761561867ce5982cc88c)
- M1.2.1 final source head [`c969aa842ad4c4565eb7fcafd51b54d32c3520f4`](https://github.com/ThresholdOps/MotiveForce/commit/c969aa842ad4c4565eb7fcafd51b54d32c3520f4)
- M1.2.1 squash merge commit [`034cdcd4c680d23bcd68b8ad959d0c4163532d9c`](https://github.com/ThresholdOps/MotiveForce/commit/034cdcd4c680d23bcd68b8ad959d0c4163532d9c)

## Decisions created

- [DEC-0005](../decisions/DEC-0005-record-envelope-revision-semantics.md), Accepted.
- [DEC-0006](../decisions/DEC-0006-deterministic-semantic-compiler-replay.md), Accepted through merge of PR #23.

## Outcome

Proposed and in progress at the design-program level. M1.2.1 and M1.2.2 design-contract work are completed, M1.2 as a whole is not completed, other items remain deferred, and no runtime implementation has started.

## Follow-up

- [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16): record envelope and revision semantics, completed as M1.2.1 design work.
- [Issue #17](https://github.com/ThresholdOps/MotiveForce/issues/17): deterministic compiler replay contract, completed through merge of PR #23.
- [Issue #18](https://github.com/ThresholdOps/MotiveForce/issues/18): diagnostic severity and aggregation; possible next candidate for a separate conscious start, but open, deferred, and not started here.
- [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19): AnalystDecision staleness, invalidation, revalidation, and controlled authority carry-forward. This remains open, deferred, and not started; it is non-blocking for M1.2.1 design acceptance but blocking before implementation of authoritative current effective-status derivation or controlled carry-forward.
- [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20): mapping-rule references and BPMN profile propagation, downstream of the accepted M1.2.2 replay requirements.
- [Issue #21](https://github.com/ThresholdOps/MotiveForce/issues/21): expanded Process IR contract test matrix.
- [Issue #8](https://github.com/ThresholdOps/MotiveForce/issues/8): detailed partial-compilation dependency policy retained from earlier open-item registration.
