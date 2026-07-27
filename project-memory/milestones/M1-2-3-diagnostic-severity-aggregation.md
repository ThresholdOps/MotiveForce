# M1.2.3: Process IR Diagnostic Severity and Aggregation Policy

- Milestone ID: `M1.2.3`
- Title: Process IR Diagnostic Severity and Aggregation Policy
- Decision status: Accepted
- Milestone status: Completed
- Implementation status: Design contract completed; runtime implementation not started
- Tracking Issue: [Issue #18](https://github.com/ThresholdOps/MotiveForce/issues/18)
- Active branch: `design/m1-2-3-diagnostic-policy`
- Delivery PR: [PR #24](https://github.com/ThresholdOps/MotiveForce/pull/24)
- Base `main`: [`a63858354f6e34f7b56900dd5a89d04ac0b19cb5`](https://github.com/ThresholdOps/MotiveForce/commit/a63858354f6e34f7b56900dd5a89d04ac0b19cb5)
- Initial source head before self-provenance amend: [`36d2a0208651e87f83a16fe13b42ebaa7d7a8961`](https://github.com/ThresholdOps/MotiveForce/commit/36d2a0208651e87f83a16fe13b42ebaa7d7a8961)
- Human review round 1: [REV-0007](../reviews/M1-2-3-diagnostic-severity-aggregation-review.md), Request changes against [`8aadf16124bd354590c3e9457f4dc0228edea258`](https://github.com/ThresholdOps/MotiveForce/commit/8aadf16124bd354590c3e9457f4dc0228edea258)
- Final human review: [REV-0008](../reviews/M1-2-3-diagnostic-severity-aggregation-review-2.md), Approve against semantic head [`fe96e20bf927927fc6fd9e34b9c475b2ad0a1af4`](https://github.com/ThresholdOps/MotiveForce/commit/fe96e20bf927927fc6fd9e34b9c475b2ad0a1af4)

## Objective

Establish the accepted Process IR diagnostic severity and aggregation policy needed before machine representation or implementation.

## Scope

- Exactly three normative severity values.
- Severity and blocking separation.
- Scope-local and operation-specific blocking.
- Complete registry of 76 accepted diagnostic codes.
- Per-code severity and blocking rules.
- Semantic diagnostic identity.
- Aggregation, deduplication, and multiplicity.
- Deterministic non-semantic ordering.
- Compilation and replay outcome derivation.
- Partial-compilation and exact-replay compatibility.
- Synthetic examples and manual review tests.

## Explicit non-goals

- No schema or programming-language model.
- No compiler, diagnostic engine, aggregation engine, or Replay Verifier.
- No runtime logging, API, persistence, database, or UI design.
- No executable validation, test implementation, or CI.
- No hash algorithm or canonical serialization.
- No start of Issues #8 or #19-#21.

## Deliverables

- Accepted [Diagnostic Policy Contract](../../docs/PROCESS_IR_DIAGNOSTIC_POLICY_CONTRACT.md).
- Accepted [DEC-0007](../decisions/DEC-0007-process-ir-diagnostic-severity-aggregation.md).
- M1.2.3 and project-memory status synchronization.
- Issue #18 and PR provenance.

Human review round 1 is recorded in [REV-0007](../reviews/M1-2-3-diagnostic-severity-aggregation-review.md). Final approval is recorded in [REV-0008](../reviews/M1-2-3-diagnostic-severity-aggregation-review-2.md), which closes all four REV-0007 findings.

## Acceptance criteria

Completion is established through merge of PR #24 with:

- complete and faithful per-code registry,
- final human semantic and design approval in REV-0008,
- accepted severity, blocking, aggregation, ordering, and outcome rules,
- Diagnostic Policy Contract status changed to `Accepted`,
- DEC-0007 changed to `Accepted`,
- merge of the delivery PR,
- project-memory synchronization recording the accepted result.

The design-contract completion conditions are approved by REV-0008 and become repository-authoritative through merge of PR #24. The actual squash merge SHA remains authoritative in GitHub metadata and is not predicted here.

## Dependencies

- M1 is Accepted and Completed.
- M1.2.1 is Accepted and Completed.
- M1.2.2 is Accepted and Completed.
- Issue #18 consumes all three accepted diagnostic catalogues.
- Issue #8 remains responsible for detailed partial-compilation dependency closure.
- Issue #19 remains responsible for staleness and invalidation triggers.
- Issue #20 remains responsible for mapping and target-profile details.
- Issue #21 remains responsible for the expanded test matrix.

## Human review

REV-0007 requested four bounded corrections. REV-0008 approves the corrected semantic head, answers all eight review questions affirmatively, and closes `REV7-FIND-001` through `REV7-FIND-004`.

## Outcome

Accepted and completed as design-contract work through merge of PR #24. Issue #18 closes only after successful merge. No schema, compiler, diagnostic engine, aggregation engine, runtime, API, persistence, tests, or CI has started.

## Follow-up

- Record the final source head in PR #24 and Issue #18 metadata.
- Close Issue #18 after successful merge.
- Keep M1.2 as a whole not completed.
- Keep Issues #8 and #19-#21 open and not started.
