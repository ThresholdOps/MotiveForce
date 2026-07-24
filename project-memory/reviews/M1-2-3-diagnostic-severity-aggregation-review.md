# REV-0007: M1.2.3 Diagnostic Severity and Aggregation Review

- Review ID: `REV-0007`
- Reviewed artifact: [docs/PROCESS_IR_DIAGNOSTIC_POLICY_CONTRACT.md](../../docs/PROCESS_IR_DIAGNOSTIC_POLICY_CONTRACT.md)
- Reviewed commit: [`8aadf16124bd354590c3e9457f4dc0228edea258`](https://github.com/ThresholdOps/MotiveForce/commit/8aadf16124bd354590c3e9457f4dc0228edea258)
- Review date: 2026-07-27T09:56:04Z
- Review type: Human semantic and design review
- Reviewer authority: Human project semantic and design review supplied with the correction instruction
- Review status: Completed
- Review outcome: Request changes
- Decision effect: No acceptance, no merge authorization
- Related PR: Draft [PR #24](https://github.com/ThresholdOps/MotiveForce/pull/24)
- Related Issue: [Issue #18](https://github.com/ThresholdOps/MotiveForce/issues/18)

## Summary

The proposed M1.2.3 diagnostic severity and aggregation policy at `8aadf16124bd354590c3e9457f4dc0228edea258` received human semantic and design review.

The overall architecture is retained. The review identifies four bounded blocking corrections: preserve accepted per-code conditional blocking, make emitted report ordering normative, make same-policy replay mismatch derivation determinate, and separate unresolved replay basis from a changed exact basis.

The corrected successor commit is not accepted by this review and requires human semantic and design re-review. Author self-check after correction is not human acceptance.

DEC-0007 remains `Proposed`. M1.2.3 remains `Proposed / In progress / not completed`.

## Findings

| Finding ID | Finding | Blocking reason | Required correction |
| --- | --- | --- | --- |
| `REV7-FIND-001` | The global non-blocking `error` boundary is narrower than accepted per-code conditions. | An error within a broader operation could be made blocking even when its exact required-value, required-relation, interpretation, integrity, mapping, or policy trigger is inactive. | Define blocking conjunctively from the exact per-code condition, exact diagnostic instance, and intersection with the authoritative operation or its required dependency closure. |
| `REV7-FIND-002` | The deterministic report order uses `SHOULD`. | Two conforming emitted report views could use different orders despite the declared deterministic view. | Require every report view emitted under the exact policy to use the defined order while keeping order outside semantic identity. |
| `REV7-FIND-003` | Same-policy semantic projection differences only `MAY` produce replay mismatch. | Comparable completed executions could derive different outcomes from the same projection difference. | Require `semantic mismatch` for unequal semantic projections under the same exact comparable basis and policy, while preserving separate not-comparable, not-replayable, and execution-failed boundaries. |
| `REV7-FIND-004` | `COMPILER_IMPLEMENTATION_UNRESOLVED` mixes unresolved identity with a different exact identity. | Missing or insufficient basis and changed exact basis have distinct accepted replay outcomes. | Map unresolved compiler identity only to `not replayable`; use `REPLAY_NOT_COMPARABLE` and `not comparable` when both exact identities are available but differ. |

No additional blocking findings are supplied by this review.

## Non-findings retained

The following are not separate blocking findings:

- the three-level severity vocabulary,
- all 76 inherited diagnostics being Proposed as `error`,
- `warning` and `info` remaining unused by the current inherited inventory,
- semantic diagnostic identity fields,
- provenance-preserving deduplication,
- non-semantic multiplicity,
- no count-based escalation,
- derived summaries,
- scope-local partial compilation,
- deferred trigger algorithms belonging to Issues #8, #19, and #20,
- absence of a machine schema or implementation.

These areas remain subject to final review but require no separate correction from REV-0007.

## Review disposition

- Overall architecture: retained.
- Required corrections: four bounded semantic clarifications.
- Diagnostic policy contract: remains `Proposed`.
- DEC-0007: remains `Proposed`.
- M1.2.3: remains `Proposed / In progress / not completed`.
- PR #24: remains Draft.
- Issue #18: remains open and In progress.
- Acceptance: not granted.
- Merge authorization: not granted.
- Corrected successor: requires human semantic and design re-review.

## Remaining review questions

1. Is the three-level severity vocabulary sufficient?
2. Is the separation between severity and blocking correct?
3. Is the complete per-code registry faithful to accepted M1, M1.2.1, and M1.2.2 semantics?
4. Are aggregation, deduplication, and multiplicity rules sufficiently determinate?
5. Is compilation outcome derivation compatible with accepted partial-compilation rules?
6. Is replay comparison compatible with the accepted M1.2.2 diagnostic projection?
7. Is deterministic report ordering adequate without making ordering semantic?
8. Is the Proposed design ready for acceptance?
