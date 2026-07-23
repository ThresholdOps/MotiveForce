# M1: Process IR Contract

- Milestone ID: `M1`
- Title: Process Intermediate Representation Contract
- Status: Completed
- Document status: Accepted

## Objective

Define the semantic contract between the probabilistic Analytical Agent and deterministic Semantic Compiler before BPMN Kernel implementation begins.

## Scope

- One document merged through PR #2: `docs/PROCESS_IR_CONTRACT.md`.
- No code.
- No machine schema.
- No BPMN Kernel implementation.

## Explicit non-goals

- Runtime parser, compiler, validator, kernel, UI, persistence, or export adapter.
- JSON Schema or other machine-readable Process IR schema.
- Full BPMN mapping catalogue.

## Deliverables

- Accepted Process IR contract in [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2).

## Acceptance basis

M1 is accepted. PR #2 was squash-merged after conditional human acceptance. The review basis and provenance qualification are recorded in [REV-0001](../reviews/M1-process-ir-semantic-review.md).

## Related PRs

- [PR #2: M1: define the Process IR contract](https://github.com/ThresholdOps/MotiveForce/pull/2)

## Related commits

- Original Draft commit [`34d2ccfa752ef10742ccf2e81f0e09757c11a240`](https://github.com/ThresholdOps/MotiveForce/commit/34d2ccfa752ef10742ccf2e81f0e09757c11a240)
- Amended Draft commit [`f32543d778af2dbbdf1d5f48565cf3e141819f67`](https://github.com/ThresholdOps/MotiveForce/commit/f32543d778af2dbbdf1d5f48565cf3e141819f67)
- Focused-correction Draft commit [`96c2d1ee50f876a8fd0d895b72770e0faf92427c`](https://github.com/ThresholdOps/MotiveForce/commit/96c2d1ee50f876a8fd0d895b72770e0faf92427c)
- Final-hardening Draft commit [`59f1cde14c118bc8f0dcc0e1d6ebc2784a2ec600`](https://github.com/ThresholdOps/MotiveForce/commit/59f1cde14c118bc8f0dcc0e1d6ebc2784a2ec600)
- Final accepted source head [`b2d6fe8f2192149145e04cbf2f0e5ffea737e1c0`](https://github.com/ThresholdOps/MotiveForce/commit/b2d6fe8f2192149145e04cbf2f0e5ffea737e1c0)
- Squash merge commit [`54d5e814601788574d13761561867ce5982cc88c`](https://github.com/ThresholdOps/MotiveForce/commit/54d5e814601788574d13761561867ce5982cc88c)

## Decisions created

- [DEC-0002](../decisions/DEC-0002-agent-compiler-kernel-authority.md) is Accepted.

## Review cycles

- Author self-check completed in PR #2.
- First human semantic review requested corrections.
- Amended commit `f32543d...` applied corrections.
- Second human semantic review requested focused corrections.
- Commit `96c2d1e...` applied focused corrections.
- Final M1 semantic-hardening review requested explicit context, decision authority, compiled semantic model, diagnostic separation, partial-compilation policy, decision outcomes, target BPMN profile propagation, and required versus not-applicable corrections.
- Commit `59f1cde...` applied final hardening.
- Final normative corrections consolidated ambiguity into `AMBIGUOUS_BUSINESS_MEANING`, made refusal scope-local, prevented event-trigger bypass through mapping choices, and corrected list punctuation.
- Final source head `b2d6fe8...` recorded document status `Accepted`; acceptance provenance is qualified in [REV-0001](../reviews/M1-process-ir-semantic-review.md).
- PR #2 was squash-merged as `54d5e81...`.

## Accepted semantic scope

- `SemanticContext` and `context_ref` rules.
- `DecisionAuthorityRef` and M1 human authority constraints.
- `CompiledSemanticModel` boundary.
- Business-versus-modeling diagnostics.
- Explicit partial-compilation policy.
- `AnalystDecision.decision_outcome`.
- `target_bpmn_profile` propagation.
- Required versus not-applicable semantics.
- `AMBIGUOUS_BUSINESS_MEANING` as the single normative compiler diagnostic for unresolved business ambiguity.
- Scope-local refusal behavior compatible with explicitly enabled partial compilation.
- Event-trigger semantics cannot be bypassed through modeling or mapping choices.

## Expected completion condition

M1 is completed by merged PR #2 and accepted document status.

## Outcome

Completed.

## Follow-up

Decide whether to create a machine-readable Process IR schema path or first validate the accepted semantic contract manually against the reference scenario.

Tracking: [Issue #4](https://github.com/ThresholdOps/MotiveForce/issues/4).

Future hardening is registered as [M1.2](M1-2-process-ir-machine-readiness.md) and [M2](M2-machine-schema-contract-validation.md).
