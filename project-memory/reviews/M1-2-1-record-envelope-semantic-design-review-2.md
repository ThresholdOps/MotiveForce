# REV-0003: M1.2.1 RecordEnvelope Semantic and Design Re-Review

- Review ID: `REV-0003`
- Reviewed artifact: [docs/PROCESS_IR_RECORD_ENVELOPE_CONTRACT.md](../../docs/PROCESS_IR_RECORD_ENVELOPE_CONTRACT.md)
- Reviewed commit: [`ed05f15dd42d95b3c38d56ae0ca19e39d783ee08`](https://github.com/ThresholdOps/MotiveForce/commit/ed05f15dd42d95b3c38d56ae0ca19e39d783ee08)
- Review date: 2026-07-23T13:06:47Z
- Review type: Human semantic and design re-review
- Reviewer authority: Human project semantic and design review
- Review status: Completed
- Review outcome: Request changes
- Decision effect: No acceptance, no merge authorization
- Related PR: Draft [PR #22](https://github.com/ThresholdOps/MotiveForce/pull/22)
- Related Issue: [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16)
- Prior review record: [REV-0002](M1-2-1-record-envelope-semantic-design-review.md)

## Summary

The proposed M1.2.1 RecordEnvelope and revision-semantics contract at `ed05f15dd42d95b3c38d56ae0ca19e39d783ee08` was reviewed after the first review corrections.

The six blocking findings from REV-0002 are considered materially addressed and are not reopened by this review. The overall RecordEnvelope architecture is retained for continued drafting.

This review requests three bounded corrections. The corrected successor commit has not received human acceptance. Author self-check after correction will not constitute acceptance.

DEC-0005 remains `Proposed`. M1.2.1 remains `Proposed / In progress / not completed`.

## Findings

| Finding ID | Finding | Blocking reason | Required correction |
| --- | --- | --- | --- |
| `REV3-FIND-001` | The reviewed four-axis preservation assertion needs clearer authority and representation. | A preservation assertion could be mistaken for self-authorizing metadata on the successor revision. | Define preservation as a separately identifiable exact revisioned basis record or equivalent exact revisioned semantic record, with exact basis references and authority where accepted meaning is affected. |
| `REV3-FIND-002` | Exact-reference handling for authoritative bases outside Process IR is too narrow. | External authority, context, policy, rule, profile, or mapping bases could remain floating even when subject revisions are exact. | Generalize the external exact-reference rule to every external authoritative basis without inventing Process IR revision IDs for external artifacts. |
| `REV3-FIND-003` | Effective-status derivation needs a current-status boundary while Issue #19 remains unresolved. | Exact closed references support historical replay but do not prove that a status remains authoritative now. | Limit authoritative current effective-status derivation until an Accepted staleness and invalidation policy exists; emit a blocking diagnostic when current staleness cannot be determined. |

## Review conclusions

- `REC-CHOICE-005`: semantically acceptable as the conservative default. No automatic authority or acceptance carry-forward between revisions. Detailed controlled carry-forward remains deferred to [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19). DEC-0005 still remains Proposed until final human re-review and merge.
- `REC-CHOICE-009`: acceptable in principle, subject to the preservation-assertion clarification required by `REV3-FIND-001`.
- Exact basis requirements: acceptable for authoritative use, subject to the generalized external-reference rule required by `REV3-FIND-002`.
- Effective-status derivation: sufficient for exact historical or as-of derivation, but insufficient for authoritative current-status derivation without the unresolved-staleness boundary required by `REV3-FIND-003`.

## Non-blocking conclusion

Identity split, immutability, explicit branching, authorship and authority separation, integrity-only digests, separation of `RevisionLineage` and `RecordDerivationGraph`, subject/status-basis separation, and refusal of silent "latest" remain directionally accepted for continued drafting.

None of those points is formally `Accepted` until later human review and merge.

## Remaining review questions

- Whether the corrected preservation assertion model is authoritative enough without becoming self-authorizing metadata.
- Whether generalized external exact-reference requirements are practical for every authoritative external basis.
- Whether the boundary between historical/as-of derivation and current effective-status derivation is sufficiently conservative while Issue #19 remains open.
- Whether DEC-0005 can be accepted after the bounded corrections are applied.
