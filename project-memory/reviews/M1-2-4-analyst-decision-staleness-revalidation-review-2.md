# REV-0010: M1.2.4 AnalystDecision Staleness and Revalidation Final Review

- Review ID: `REV-0010`
- Reviewed artifact: [docs/ANALYST_DECISION_STALENESS_REVALIDATION_CONTRACT.md](../../docs/ANALYST_DECISION_STALENESS_REVALIDATION_CONTRACT.md)
- Reviewed semantic head: [`4463aafca5e5fa176bcd3bb0db604b0a48943d9b`](https://github.com/ThresholdOps/MotiveForce/commit/4463aafca5e5fa176bcd3bb0db604b0a48943d9b)
- Review date: 2026-07-27T12:04:00Z
- Review type: Human semantic and design final re-review
- Reviewer authority: Human project semantic and design approval supplied with the finalization instruction
- Review status: Completed
- Review outcome: Approve
- Prior review: [REV-0009](M1-2-4-analyst-decision-staleness-revalidation-review.md)
- Decision effect: M1.2.4 contract and DEC-0008 approved; M1.2.4 approved for completion through PR #25 merge; merge authorized after bounded finalization validation
- Implementation effect: None; implementation remains not started
- Related PR: [PR #25](https://github.com/ThresholdOps/MotiveForce/pull/25)
- Related Issue: [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19)

## Review boundary

The full human semantic and design final re-review was performed against semantic head `4463aafca5e5fa176bcd3bb0db604b0a48943d9b`.

The subsequent source amendment is limited to the authorized review record, status transitions, governance synchronization, indexing, PR and Issue provenance, and merge preparation. No independent full semantic reread of that amended source head is claimed. Any normative semantic change beyond the reviewed head invalidates this approval and must stop the delivery.

## Review conclusions

### Historical validity and current authority

Approved. Historical authority is a derived authority assessment and preserved provenance fact for an exact original basis. It is not source evidence, proof of business truth, or present authority for a changed request. Historical and current invalidity remain separate.

### Current-authority outcome model

Approved. Exactly these four derived outcomes are Accepted:

- `current-authoritative`
- `revalidation-required`
- `invalidated-for-current-use`
- `unresolved`

They are not M1 lifecycle states or mutable fields.

### Exact basis closure

Approved. The `AnalystDecisionBasisSet` closes every applicable exact subject, evidence, dependency, context, authority, status, impact, relevance, value-state, policy, external-basis, and request reference. Floating or implicit authoritative bases remain forbidden.

### Relevance dispositions

Approved. Every detected basis change requires exactly one disposition: `relevant`, `not-relevant`, or `undetermined`.

- Omission is not `not-relevant`.
- A fully applicable Accepted deterministic rule may derive relevance.
- Material semantic judgment must be human-authorized.
- The Analytical Agent may propose a disposition but cannot authoritatively preserve current authority through a `not-relevant` judgment.
- Incomplete or undetermined relevance produces `unresolved`.

### Staleness and non-trigger rules

Approved. Relevant semantic, contextual, evidence, dependency, authority, and review-condition changes produce the defined revalidation or invalidation outcome. Age alone, unrelated evidence, presentation metadata, compiler, mapping, target-profile, rendering, and equivalent BPMN representation changes do not stale business meaning by themselves.

### Derived and explicit invalidation

Approved. Derived current-use invalidation follows directly from exact bases and exact policy, requires no synthetic status record, and preserves historical provenance.

An explicit invalidation or revocation act changes the status basis, requires a separate exact revisioned basis and valid authority, and is scoped by context, time, and affected decision.

### Revalidation and controlled carry-forward

Approved. Revalidation is a new exact human-authorized basis, never mutation. Controlled carry-forward is explicit, exact, named, scoped, human-authorized, and non-transitive. It does not automatically preserve four-axis value state, establish BPMN validity or mapping eligibility, or authorize another scope or actor.

### Effective status and diagnostics

Approved. Only `current-authoritative` decisions may act as authoritative current status bases. Stale, invalidated, or unresolved authority cannot be bypassed through partial compilation. The 18-code diagnostic crosswalk is Accepted without code, severity, or blocking-rule changes. Value-state reevaluation remains separate from `AnalystDecision` revalidation.

### Identity, partial-compilation, and replay boundaries

Approved.

- Issue #6 retains technical identity representation.
- Issue #8 retains detailed partial-compilation dependency closure.
- Replay reproduces historical assessments only against exact historical bases and policy.
- Historical replay does not establish present authority.
- No Replay Verifier is created.

## Finding closure

| Finding ID | Final disposition | Basis |
| --- | --- | --- |
| `REV9-FIND-001` | Closed | Historical authority is a derived assessment and provenance fact, not source evidence or business truth. |
| `REV9-FIND-002` | Closed | Every detected basis change requires an exact authorized relevance disposition; omission cannot preserve authority. |
| `REV9-FIND-003` | Closed | Policy-derived invalidation is separated from explicit authorized invalidation or revocation acts. |
| `REV9-FIND-004` | Closed | Missing authority, stale revision, and value-state diagnostics retain distinct current-authority outcomes. |

No new findings are created by REV-0010.

## Design-choice decisions

- `STALE-CHOICE-001` through `STALE-CHOICE-010` are Accepted.
- `STALE-CHOICE-002`, `STALE-CHOICE-005`, `STALE-CHOICE-008`, and `STALE-CHOICE-010`, previously classified as Potential semantic changes, are explicitly accepted by human semantic and design review.
- Exact authorized relevance-disposition behavior is accepted as part of the staleness-relevance and unresolved-authority policy.
- The four-outcome model is accepted.
- Controlled carry-forward is accepted only within its exact, human-authorized, non-transitive boundary.

No implementation algorithm or machine representation is selected.

## Decision effect

- M1.2.4 contract: Approved; repository-authoritative acceptance becomes effective through merge of PR #25.
- DEC-0008: Approved; repository-authoritative acceptance becomes effective through merge of PR #25.
- M1.2.4: Approved for design-contract completion through merge of PR #25.
- Merge authorization: Granted after bounded finalization validation.
- Implementation authorization: None.

All eight human-review questions are answered `Yes`.
