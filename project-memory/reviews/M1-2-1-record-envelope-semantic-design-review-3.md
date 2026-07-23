# REV-0004: M1.2.1 RecordEnvelope Final Semantic and Design Review

- Review ID: `REV-0004`
- Reviewed artifact: [docs/PROCESS_IR_RECORD_ENVELOPE_CONTRACT.md](../../docs/PROCESS_IR_RECORD_ENVELOPE_CONTRACT.md)
- Reviewed semantic head: [`b4c29bb8505db099feeb58afc3ec5755f90e85e8`](https://github.com/ThresholdOps/MotiveForce/commit/b4c29bb8505db099feeb58afc3ec5755f90e85e8)
- Review date: 2026-07-23T15:23:10Z
- Review type: Human semantic and design final re-review
- Reviewer authority: Human project semantic and design approval supplied with the finalization instruction
- Review status: Completed
- Review outcome: Approve
- Decision effect: M1.2.1 design approved; DEC-0005 approved; merge authorized after bounded finalization validation; acceptance becomes repository-authoritative through merge of [PR #22](https://github.com/ThresholdOps/MotiveForce/pull/22)
- Related Issue: [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16)
- Related decision: [DEC-0005](../decisions/DEC-0005-record-envelope-revision-semantics.md)
- Prior review records: [REV-0002](M1-2-1-record-envelope-semantic-design-review.md), [REV-0003](M1-2-1-record-envelope-semantic-design-review-2.md)

## Review basis

This record memorializes the human decision supplied with the execution instruction for finalizing M1.2.1. Creation of REV-0004 is not an author self-review.

The human semantic and design review was completed for corrected M1.2.1 head `b4c29bb8505db099feeb58afc3ec5755f90e85e8` with outcome `Approve`.

The final bounded amendment may contain only the review record, status changes, finding closures, decision and milestone finalization, Issue #19 boundary wording, project-memory synchronization, PR and Issue metadata preparation, and directly required formatting or link corrections.

The final amended source head is authoritative in PR #22 metadata after push. The final amended head must not be described as receiving a separate independent full semantic reread unless such a review actually occurred. Human approval of `b4c29bb...` includes authorization for the bounded finalization changes listed in the execution instruction.

## Accepted scope

The human decision explicitly accepts:

- the M1.2.1 RecordEnvelope and revision-semantics design,
- `REC-CHOICE-005` as the conservative no-automatic-authority-carry-forward default,
- `REC-CHOICE-009` and the reviewed preservation-assertion model,
- generalized exact-reference requirements for external authoritative bases,
- the boundary between historical/as-of effective-status derivation and authoritative current-status derivation,
- all corrections introduced for REV-0002 and REV-0003.

## Finding closure

| Finding ID | Final disposition | Basis |
| --- | --- | --- |
| `REV2-FIND-001` through `REV2-FIND-006` | Closed. | The six REV-0002 findings were materially addressed by the corrected design and accepted by this final review. |
| `REV3-FIND-001` | Closed. | The reviewed preservation assertion is accepted as a separately identifiable exact revisioned basis record or equivalent exact revisioned semantic record. It is not a Boolean flag or self-authorizing successor metadata; it references exact predecessor assessment, successor subject revision, both semantic basis sets, exact context, revision-impact classification, and required authority. `VALUE_STATE_PRESERVATION_BASIS_INVALID` is accepted. |
| `REV3-FIND-002` | Closed. | External authoritative bases are accepted when made exact through immutable external locator, explicit version identifier, immutable content identifier, or versioned locator plus integrity descriptor where applicable. `current`, `latest`, unversioned mutable URLs, silent repository-head resolution, and other floating external authoritative bases remain rejected. `FLOATING_EXTERNAL_BASIS` is accepted. |
| `REV3-FIND-003` | Closed. | The contract distinguishes historical/as-of derivation against an exact closed basis set from authoritative current-status derivation requiring an Accepted staleness policy. `EFFECTIVE_STATUS_STALENESS_UNDETERMINED` is accepted as blocking for unresolved current authority. Exact reference resolution is necessary but not sufficient for current validity; the Semantic Compiler cannot bypass the condition through partial compilation, and the BPMN Kernel cannot resolve it. |

## Design-choice decisions

- `REC-CHOICE-005`: Accepted. Acceptance attaches to exact revisions identified by authoritative decision records. A new revision does not automatically inherit acceptance or authority. Controlled confirmation or carry-forward may only be introduced by a later Accepted policy, and detailed controlled carry-forward remains assigned to [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19).
- `REC-CHOICE-009`: Accepted. Four-axis value-state assessments remain revision-scoped; preservation requires the accepted exact reviewed preservation-assertion model; omission does not mean inheritance; cross-revision axis composition remains prohibited without a later Accepted aggregation contract.
- `REC-CHOICE-013`: Accepted as part of the approved contract.
- `REC-CHOICE-014`: Accepted as part of the approved contract.

## Remaining boundary

No semantic blocker remains for M1.2.1.

[Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19) remains open and not started. It is non-blocking for M1.2.1 design acceptance and for exact historical/as-of derivation design. It is blocking before implementation of authoritative current effective-status derivation, AnalystDecision staleness, invalidation, revalidation, or controlled authority carry-forward.

No schema, code, runtime, API, persistence, executable validation, tests, CI, or dependency change is authorized by this review.
