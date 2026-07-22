# DEC-0003: Process IR Before BPMN Kernel

- ID: `DEC-0003`
- Title: Define Process IR before BPMN Kernel implementation
- Status: Accepted
- Date: 2026-07-22T19:29:33Z
- Decision authority: Merged repository content in [PR #1](https://github.com/ThresholdOps/MotiveForce/pull/1)

## Context

The first unresolved architectural problem named in the merged README is the contract between the Analytical Agent and the Semantic Compiler.

## Decision

The minimal data contract between the Analytical Agent and the Semantic Compiler must be defined before BPMN Kernel implementation begins.

## Rationale

The merged README states that no BPMN Kernel implementation should begin before this boundary is defined. This enforces the rule that the LLM does not validate BPMN structurally rather than only by prompt instruction.

## Alternatives considered

- Begin BPMN Kernel implementation first: rejected by merged M0 next-step statement.
- Generate XML directly from agent output: rejected by the canonical-model thesis.
- Delay the Process IR boundary until after UI work: deferred by the current architecture sequence.

## Consequences

- M1 focuses on `docs/PROCESS_IR_CONTRACT.md`.
- Kernel implementation remains out of scope until later M1.2/M2 machine-readiness and BPMN Kernel decisions.
- The Process IR contract is accepted in merged PR #2, satisfying this decision's immediate ordering requirement.

## Related artifacts

- [README.md](../../README.md)
- [PR #1](https://github.com/ThresholdOps/MotiveForce/pull/1)
- Merge commit [`5c3350bde99fde4c3420902856d37a2800ebbea7`](https://github.com/ThresholdOps/MotiveForce/commit/5c3350bde99fde4c3420902856d37a2800ebbea7)
- Merged [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2)
- M1 source head [`b2d6fe8f2192149145e04cbf2f0e5ffea737e1c0`](https://github.com/ThresholdOps/MotiveForce/commit/b2d6fe8f2192149145e04cbf2f0e5ffea737e1c0)
- M1 merge commit [`54d5e814601788574d13761561867ce5982cc88c`](https://github.com/ThresholdOps/MotiveForce/commit/54d5e814601788574d13761561867ce5982cc88c)

## Supersedes

None.

## Superseded by

None.

## Follow-up actions

- Decide whether to move to schema design or manual scenario validation.
