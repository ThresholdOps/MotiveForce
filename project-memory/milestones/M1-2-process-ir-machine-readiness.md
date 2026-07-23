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

M1.2 is not completed. M1 semantic acceptance is satisfied by merged PR #2. M1.2 has consciously started through the narrow M1.2.1 RecordEnvelope and revision-semantics design work tracked by [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16). M1.2.1 is accepted and completed as design-contract work through [PR #22](https://github.com/ThresholdOps/MotiveForce/pull/22), but other M1.2 Issues remain deferred.

## Related PRs

- Merged [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2) defines the accepted M1 semantic contract.
- [PR #3](https://github.com/ThresholdOps/MotiveForce/pull/3) registers this milestone record.
- [PR #22](https://github.com/ThresholdOps/MotiveForce/pull/22) completes M1.2.1 design-contract work.

## Related commits

- M1 final source head [`b2d6fe8f2192149145e04cbf2f0e5ffea737e1c0`](https://github.com/ThresholdOps/MotiveForce/commit/b2d6fe8f2192149145e04cbf2f0e5ffea737e1c0)
- M1 merge commit [`54d5e814601788574d13761561867ce5982cc88c`](https://github.com/ThresholdOps/MotiveForce/commit/54d5e814601788574d13761561867ce5982cc88c)

## Decisions created

- [DEC-0005](../decisions/DEC-0005-record-envelope-revision-semantics.md), Accepted.

## Outcome

Proposed and in progress at the program level. M1.2.1 design work is completed, M1.2 as a whole is not completed, and no runtime implementation has started.

## Follow-up

- [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16): record envelope and revision semantics, completed as M1.2.1 design work.
- [Issue #17](https://github.com/ThresholdOps/MotiveForce/issues/17): deterministic compiler replay contract.
- [Issue #18](https://github.com/ThresholdOps/MotiveForce/issues/18): diagnostic severity and aggregation.
- [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19): AnalystDecision staleness, invalidation, revalidation, and controlled authority carry-forward. This remains open, deferred, and not started; it is non-blocking for M1.2.1 design acceptance but blocking before implementation of authoritative current effective-status derivation or controlled carry-forward.
- [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20): mapping-rule references and BPMN profile propagation.
- [Issue #21](https://github.com/ThresholdOps/MotiveForce/issues/21): expanded Process IR contract test matrix.
- [Issue #8](https://github.com/ThresholdOps/MotiveForce/issues/8): detailed partial-compilation dependency policy retained from earlier open-item registration.
