# REV-0005: M1.2.2 Deterministic Semantic Compiler Replay Review

- Review ID: `REV-0005`
- Reviewed artifact: [docs/SEMANTIC_COMPILER_REPLAY_CONTRACT.md](../../docs/SEMANTIC_COMPILER_REPLAY_CONTRACT.md)
- Reviewed commit: [`7f70e0aeea17a0b1432bfb2c73ec496950f75ac7`](https://github.com/ThresholdOps/MotiveForce/commit/7f70e0aeea17a0b1432bfb2c73ec496950f75ac7)
- Review date: 2026-07-24T12:00:32Z
- Review type: Human semantic and design review
- Reviewer authority: Human project semantic and design review
- Review status: Completed
- Review outcome: Request changes
- Decision effect: No acceptance, no merge authorization
- Related PR: Draft [PR #23](https://github.com/ThresholdOps/MotiveForce/pull/23)
- Related Issue: [Issue #17](https://github.com/ThresholdOps/MotiveForce/issues/17)

## Summary

The proposed M1.2.2 deterministic Semantic Compiler replay contract at `7f70e0aeea17a0b1432bfb2c73ec496950f75ac7` received human semantic and design review.

The overall deterministic replay architecture is retained. The review identifies one bounded blocking correction: define the minimum semantic comparison projection used for same-replay verification.

The corrected successor commit has not received human acceptance and requires human semantic and design re-review. Author self-check after correction is not human acceptance.

DEC-0006 remains `Proposed`. M1.2.2 remains `Proposed / In progress / not completed`.

## Finding

| Finding ID | Finding | Blocking reason | Required correction |
| --- | --- | --- | --- |
| `REV5-FIND-001` | The contract lists semantic outcome components but does not define a sufficiently explicit minimum semantic comparison projection. | Two comparison implementations could disagree about identifiers, diagnostics, ordering, textual fields, or runtime metadata while evaluating the same original and replay outputs. | Define the minimum semantic projection used by same-replay verification, including the applicable replay-contract revision, semantic identifier boundary, diagnostic projection, and excluded serialization and observational fields. |

## Non-blocking exploratory topics

The following are not separate blocking findings in this review:

- a separate Replay Verifier architecture,
- a standalone `ReplayComparisonPolicyRef`,
- a full manifest lifecycle and reconstruction model,
- a dependency-role taxonomy,
- a complete identifier taxonomy,
- additional replay diagnostics for those deferred concerns.

These topics may be revisited in M2 or implementation design if they become necessary. They are not required to correct `REV5-FIND-001`.

## Review disposition

- Overall architecture: retained.
- Required correction: one bounded semantic-comparison clarification.
- Replay contract: remains `Proposed`.
- DEC-0006: remains `Proposed`.
- M1.2.2: remains `Proposed / In progress / not completed`.
- PR #23: remains Draft.
- Issue #17: remains open and In progress.
- Acceptance: not granted.
- Merge authorization: not granted.

## Remaining review questions

- Is the semantic projection now sufficiently determinate?
- Is the semantic identifier boundary correct?
- Is the diagnostic comparison projection compatible with the future Issue #18 policy?
- Is the corrected design ready for acceptance?
