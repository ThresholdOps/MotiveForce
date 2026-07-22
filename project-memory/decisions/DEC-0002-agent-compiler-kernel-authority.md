# DEC-0002: Agent, Compiler, and Kernel Authority

- ID: `DEC-0002`
- Title: Agent, Compiler, and Kernel authority separation
- Status: Accepted
- Date: 2026-07-23T08:08:27Z
- Decision authority: Established by merged [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2) and the accepted M1 contract. The semantic-review basis and provenance qualification are recorded in [REV-0001](../reviews/M1-process-ir-semantic-review.md).

## Context

Merged M0 content states the high-level architecture boundary: the LLM interprets source material, the Semantic Compiler maps approved meaning, and the BPMN Kernel validates the resulting BPMN model. Merged M1 content accepts detailed authority rules for this boundary.

## Decision

Accepted authority separation:

- the Analytical Agent interprets source material and proposes,
- human authority accepts business meaning where required,
- the Semantic Compiler maps accepted meaning and determines mapping eligibility,
- the BPMN Kernel validates BPMN legality.

## Rationale

This separation prevents probabilistic interpretation from becoming deterministic BPMN validation.

The review record is the canonical explanation of how M1 semantic acceptance was reached. This decision record summarizes the accepted authority separation without broadening the review claim beyond [REV-0001](../reviews/M1-process-ir-semantic-review.md).

## Alternatives considered

- Agent directly validates BPMN: rejected in merged M0 thesis.
- Compiler interprets source text directly: rejected in accepted M1 contract.
- Human decision replaces BPMN validation: rejected in accepted M1 contract.

## Consequences

- Proposed records are inspectable but not authoritative compilation input.
- Mapping eligibility is separate from BPMN validity.
- Semantic context, human decision authority, compiled semantic output, partial compilation, and target BPMN profile treatment are accepted for the conceptual M1 contract.
- Machine-readiness details remain deferred to M1.2 and M2.

## Related artifacts

- [README.md](../../README.md)
- [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2)
- [REV-0001: M1 Process IR Semantic Review](../reviews/M1-process-ir-semantic-review.md)
- Prior focused-correction Draft M1 commit [`96c2d1ee50f876a8fd0d895b72770e0faf92427c`](https://github.com/ThresholdOps/MotiveForce/commit/96c2d1ee50f876a8fd0d895b72770e0faf92427c)
- Final-hardening Draft M1 commit [`59f1cde14c118bc8f0dcc0e1d6ebc2784a2ec600`](https://github.com/ThresholdOps/MotiveForce/commit/59f1cde14c118bc8f0dcc0e1d6ebc2784a2ec600)
- Final accepted source head [`b2d6fe8f2192149145e04cbf2f0e5ffea737e1c0`](https://github.com/ThresholdOps/MotiveForce/commit/b2d6fe8f2192149145e04cbf2f0e5ffea737e1c0)
- Squash merge commit [`54d5e814601788574d13761561867ce5982cc88c`](https://github.com/ThresholdOps/MotiveForce/commit/54d5e814601788574d13761561867ce5982cc88c)

## Supersedes

None.

## Superseded by

None.

## Follow-up actions

- Track machine-readiness follow-up in M1.2.
- Track machine schema and contract validation follow-up in M2.
