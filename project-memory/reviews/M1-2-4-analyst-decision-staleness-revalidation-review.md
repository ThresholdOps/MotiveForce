# REV-0009: M1.2.4 AnalystDecision Staleness and Revalidation Review

- Review ID: `REV-0009`
- Reviewed artifact: [docs/ANALYST_DECISION_STALENESS_REVALIDATION_CONTRACT.md](../../docs/ANALYST_DECISION_STALENESS_REVALIDATION_CONTRACT.md)
- Reviewed commit: [`74d288fd57810f0b1a2c7865185889f07e67146e`](https://github.com/ThresholdOps/MotiveForce/commit/74d288fd57810f0b1a2c7865185889f07e67146e)
- Review date: 2026-07-27T11:40:07Z
- Review type: Human semantic and design review
- Reviewer authority: Human project semantic and design review supplied with the correction instruction
- Review status: Completed
- Review outcome: Request changes
- Decision effect: No acceptance and no merge authorization
- Overall architecture: Retained
- Related PR: Draft [PR #25](https://github.com/ThresholdOps/MotiveForce/pull/25)
- Related Issue: [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19)

## Summary

The Proposed M1.2.4 contract at `74d288fd57810f0b1a2c7865185889f07e67146e` received human semantic and design review.

The overall architecture is retained. Four bounded corrections are required: keep authority distinct from source evidence, establish authority for relevance dispositions, separate derived current-use invalidation from explicit invalidation acts, and preserve diagnostic-to-outcome fidelity.

The corrected successor is not accepted by REV-0009 and requires human semantic and design re-review. Author self-check after correction is not human acceptance.

DEC-0008 remains `Proposed`. M1.2.4 remains `Proposed / In progress / not completed`.

## Findings

| Finding ID | Finding | Blocking reason | Required correction |
| --- | --- | --- | --- |
| `REV9-FIND-001` | The core rule describes historical authority as evidence. | This conflicts with the accepted separation among source evidence, human authority, acceptance, compilation, and BPMN validation. | Define historical authority as a derived authority assessment and provenance fact that is not source evidence, proof of business truth, or authority for a later current request. |
| `REV9-FIND-002` | The contract does not define the authority boundary for determining that a basis change is not relevant. | An omitted, agent-proposed, or otherwise unauthorized `not-relevant` classification could preserve current authority without valid review. | Require an exact `relevant`, `not-relevant`, or `undetermined` disposition for every detected change, with exact basis, scope, rationale, policy, authority, and time. |
| `REV9-FIND-003` | Derived invalidation conditions are conflated with deliberate invalidation acts that change status bases. | Requiring a synthetic status record for expiry, scope mismatch, or another exact policy-derived condition obscures the distinction between derivation and authority action. | Allow derived current-use invalidation directly from exact bases and policy; require a separate exact authorized status basis only for an explicit invalidation or revocation act. |
| `REV9-FIND-004` | Several diagnostic crosswalk rows collapse definite, unresolved, decision, and value-state conditions. | The current rows can misclassify missing authority, stale revisions, or required value-state reevaluation as the wrong current-authority outcome. | Correct `DECISION_AUTHORITY_REQUIRED`, `STALE_REVISION_REFERENCE`, `VALUE_STATE_BASIS_STALE`, and `VALUE_STATE_REEVALUATION_REQUIRED` while preserving inherited codes and blocking rules. |

No additional blocking findings are supplied by REV-0009.

## Non-findings retained

REV-0009 does not require redesign of:

- the four-outcome model,
- exact basis closure as the architectural foundation,
- historical/current separation,
- age alone as a non-trigger,
- human-authorized revalidation,
- exact and non-transitive controlled carry-forward,
- value-state preservation as a separate operation,
- the Issue #6 identity boundary,
- the Issue #8 partial-compilation boundary,
- the replay boundary,
- the 18-code diagnostic crosswalk inventory,
- diagnostic severity or aggregation,
- the example and manual-test counts,
- the absence of implementation.

These areas remain subject to final re-review but require no separate correction from REV-0009.

## Review disposition

- Contract: remains `Proposed`.
- DEC-0008: remains `Proposed`.
- M1.2.4: remains `Proposed / In progress / not completed`.
- PR #25: remains Draft and unmerged.
- Issue #19: remains open and In progress.
- Acceptance: not granted.
- Merge authorization: not granted.
- Corrected successor: requires human semantic and design re-review.

## Remaining review questions

1. Is the separation between historical validity and current authority correct?
2. Are the four current-authority assessment outcomes sufficient?
3. Are the staleness triggers and explicit non-triggers complete and correctly bounded?
4. Is the distinction between `revalidation-required` and `invalidated-for-current-use` correct?
5. Is explicit human-authorized, exact, non-transitive carry-forward sufficiently safe?
6. Is the revalidation and status-basis representation compatible with M1 and M1.2.1?
7. Are effective-status, diagnostic, partial-compilation, identity, and replay boundaries clean?
8. Is the Proposed M1.2.4 design ready for acceptance?
