# M1.2.1 RecordEnvelope Semantic and Design Review

- Review ID: `REV-0002`
- Reviewed artifact: `docs/PROCESS_IR_RECORD_ENVELOPE_CONTRACT.md`
- Reviewed commit: [`5fe3653a1ce5175841c843aa6d0196213e382341`](https://github.com/ThresholdOps/MotiveForce/commit/5fe3653a1ce5175841c843aa6d0196213e382341)
- Review type: Human semantic and design review
- Review status: Completed
- Review outcome: Request changes
- Decision effect: No acceptance, no merge authorization

## Review basis

The full proposed M1.2.1 contract at [`5fe3653a1ce5175841c843aa6d0196213e382341`](https://github.com/ThresholdOps/MotiveForce/commit/5fe3653a1ce5175841c843aa6d0196213e382341) was reviewed.

Metadata verification is not the semantic review itself. This review accepted the overall architecture for continued drafting but identified blocking corrections. The corrected successor commit has not yet received human acceptance. Author self-check after correction does not constitute acceptance.

## Blocking findings

| Finding ID | Finding | Blocking reason | Required correction |
| --- | --- | --- | --- |
| `REV2-FIND-001` | Missing exact-revision semantics for the M1 four-axis value-state model. | A revision could inherit or compose epistemic and applicability state silently. | Bind all four dimensions and their basis to exact revisions and context; require explicit preservation or reevaluation. |
| `REV2-FIND-002` | Same-record revision lineage is mixed with cross-record derivation. | Revision heads and effective revision selection become ambiguous across different logical records. | Separate `RevisionLineage` from `RecordDerivationGraph`. |
| `REV2-FIND-003` | Subject revision and status-basis revision are not explicitly separated. | Acceptance could be misread as requiring mutation or a new revision of the subject record. | Model status bases as separate exact revisioned records. |
| `REV2-FIND-004` | Conservative authority carry-forward is classified as neutral technical representation. | It defines new authority behavior not explicitly specified by M1. | Reclassify as `Potential semantic change` and leave it pending explicit human acceptance. |
| `REV2-FIND-005` | "Committed revision" boundary is undefined. | Immutability cannot be applied consistently. | Define an addressable or released revision boundary; exclude edit buffers. |
| `REV2-FIND-006` | Exact-reference rules are not explicit for all status and authority bases. | Subject records could be exact while authority, context, or evidence remains floating. | Require exact revision references for all revisioned bases used authoritatively. |

## Non-blocking conclusion

Identity split, immutability, explicit branching, authorship/authority separation, integrity-only digests, and refusal of silent "latest" remain directionally accepted for continued drafting. None is formally Accepted until a later human review and merge.

## Corrected successor

The corrected successor commit is not semantically accepted by this record. It requires human semantic and design re-review.
