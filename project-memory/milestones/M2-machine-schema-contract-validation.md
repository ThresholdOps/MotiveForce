# M2: Machine Schema and Contract Validation

- Milestone ID: `M2`
- Title: Machine Schema and Contract Validation
- Status: Proposed
- Implementation status: Deferred in current phase

## Objective

Create and validate the machine-readable Process IR contract after accepted M1 semantics and future M1.2 machine-readiness design decisions.

## Scope

- Serialization technology decision.
- Machine-readable schema.
- Schema validation.
- Compatibility rules.
- Test fixtures.
- Contract validation.
- Migration strategy.
- Deterministic replay tests where implementation exists.

## Explicit non-goals

- No schema work before relevant M1.2 decisions.
- No runtime parser, compiler, BPMN Kernel, UI, persistence, or transport implementation as part of this milestone record.
- No confidential source material.

## Deliverables

- Machine-readable Process IR schema contract design tracked by [Issue #5](https://github.com/ThresholdOps/MotiveForce/issues/5).
- Contract validation approach linked to the expanded test matrix in [Issue #21](https://github.com/ThresholdOps/MotiveForce/issues/21).

## Acceptance basis

M2 is not accepted and is not authorized as implementation work. M1 semantic acceptance is satisfied by merged PR #2; M2 remains blocked on relevant M1.2 design outcomes.

## Related PRs

- Merged [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2)
- [PR #3](https://github.com/ThresholdOps/MotiveForce/pull/3) registers this future milestone record.

## Related commits

- M1 final source head [`b2d6fe8f2192149145e04cbf2f0e5ffea737e1c0`](https://github.com/ThresholdOps/MotiveForce/commit/b2d6fe8f2192149145e04cbf2f0e5ffea737e1c0)
- M1 merge commit [`54d5e814601788574d13761561867ce5982cc88c`](https://github.com/ThresholdOps/MotiveForce/commit/54d5e814601788574d13761561867ce5982cc88c)

## Decisions created

None yet.

## Outcome

Proposed and deferred in the current phase.

## Follow-up

Reuse [Issue #5](https://github.com/ThresholdOps/MotiveForce/issues/5) as the M2 tracker for preparing the machine-readable Process IR schema contract.
