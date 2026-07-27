# DEC-0008: AnalystDecision Staleness, Invalidation, Revalidation, and Controlled Authority Carry-Forward

- ID: `DEC-0008`
- Title: AnalystDecision Staleness, Invalidation, Revalidation, and Controlled Authority Carry-Forward
- Status: Accepted
- Date: 2026-07-27T11:13:38Z
- Decision authority: Human final semantic and design approval recorded by REV-0010; repository authority established through merge of PR #25
- Related Issue: [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19)
- Related milestone: [M1.2.4](../milestones/M1-2-4-analyst-decision-staleness-revalidation.md)
- Source branch: `design/m1-2-4-analyst-decision-staleness`
- Source PR: [PR #25](https://github.com/ThresholdOps/MotiveForce/pull/25)
- Exact base: [`006574b25732f0776a7e510fd33838c9946d9677`](https://github.com/ThresholdOps/MotiveForce/commit/006574b25732f0776a7e510fd33838c9946d9677)
- Initial source head: [`377a6019afa65af9953e1f1dbcc8258416d94f50`](https://github.com/ThresholdOps/MotiveForce/commit/377a6019afa65af9953e1f1dbcc8258416d94f50)
- Final source head: To be recorded in PR and Issue metadata after the final amend
- Current review: [REV-0010](../reviews/M1-2-4-analyst-decision-staleness-revalidation-review-2.md), `Approve`

## Context

M1 defines authoritative human `AnalystDecision` and `DecisionAuthorityRef` semantics. M1.2.1 establishes immutable exact revisions, status-basis separation, exact authoritative bases, no automatic authority carry-forward, and a historical/current-status boundary. M1.2.2 and M1.2.3 establish exact replay and diagnostic behavior.

The remaining gap is a determinate policy for evaluating an exact decision after its subject, evidence, context, authority, dependencies, process version, or effective time changes.

## Accepted decision

Accept:

- separate historical validity from current authority,
- require an exact `AnalystDecisionBasisSet`,
- derive exactly one of `current-authoritative`, `revalidation-required`, `invalidated-for-current-use`, or `unresolved`,
- require an exact authorized relevance disposition for every detected basis change,
- treat relevant semantic and contextual changes as human revalidation triggers,
- treat definite authority, scope, applicability, and temporal defects as current-use invalidation,
- keep age and unrelated technical changes as non-triggers,
- derive exact policy-defined current-use invalidation without requiring a synthetic status record,
- represent revalidation and explicit invalidation or revocation acts as separate exact revisioned authority bases,
- permit controlled carry-forward only as an exact, human-authorized, non-transitive revalidation effect,
- recompute effective status without mutating the subject or original decision,
- use inherited diagnostics without changing severity or blocking behavior.

The complete accepted decision is defined by the [M1.2.4 contract](../../docs/ANALYST_DECISION_STALENESS_REVALIDATION_CONTRACT.md).

## Accepted basis

- [M1 Process IR contract](../../docs/PROCESS_IR_CONTRACT.md)
- [M1.2.1 RecordEnvelope contract](../../docs/PROCESS_IR_RECORD_ENVELOPE_CONTRACT.md)
- [M1.2.2 replay contract](../../docs/SEMANTIC_COMPILER_REPLAY_CONTRACT.md)
- [M1.2.3 Diagnostic Policy Contract](../../docs/PROCESS_IR_DIAGNOSTIC_POLICY_CONTRACT.md)
- Accepted [DEC-0005](DEC-0005-record-envelope-revision-semantics.md)
- Accepted [DEC-0006](DEC-0006-deterministic-semantic-compiler-replay.md)
- Accepted [DEC-0007](DEC-0007-process-ir-diagnostic-severity-aggregation.md)

## Rationale

Historical provenance must remain reproducible, but historical authority is a derived authority assessment and provenance fact, not source evidence or proof of business truth. It cannot silently authorize changed current meaning. Exact bases and authorized relevance dispositions make the comparison auditable. Separate outcomes distinguish reviewable change, definite invalidity, and unresolved authority without inventing a new M1 lifecycle.

Controlled carry-forward addresses bounded provenance-only and administrative corrections while preserving the accepted no-automatic-carry-forward default.

## Alternatives considered

| Alternative | Status | Reason |
| --- | --- | --- |
| Treat every old decision as currently authoritative until explicitly revoked. | Rejected in proposal. | Leaks authority across changed subjects, contexts, evidence, and time. |
| Invalidate every decision after any successor revision. | Rejected in proposal. | Conflates relevant semantic change with unrelated or administrative change. |
| Use age alone as staleness. | Rejected in proposal. | Chronology without an exact expiry or review basis is not authority. |
| Carry acceptance automatically to successor revisions. | Rejected in proposal. | Contradicts accepted M1.2.1 authority rules. |
| Allow the Analytical Agent or compiler to revalidate. | Rejected in proposal. | M1 reserves authoritative business decisions for authorized humans. |
| Mutate the original decision or subject status. | Rejected in proposal. | Violates immutable revision and status-basis separation. |
| Make controlled carry-forward transitive. | Rejected in proposal. | Would authorize unreviewed future revisions. |
| Let replay success prove current authority. | Rejected in proposal. | Reproducibility does not reauthorize historical bases. |
| Add a generic invalidation diagnostic. | Not selected. | Existing diagnostics identify the specific authority, reference, status, and staleness causes. |

## Consequences

- Current-authority evaluation requires exact original and candidate bases.
- Every detected basis change requires an exact authorized relevance disposition; omission cannot mean `not-relevant`.
- Relevant change blocks current use until human revalidation.
- Exact policy-defined authority defects derive invalidation for only the exact affected current scope without requiring a synthetic status record.
- A deliberate invalidation or revocation act requires a separate exact status basis and valid authority.
- Historical provenance and historical as-of results remain intact.
- Controlled carry-forward remains explicit, bounded, human-authorized, and non-transitive.
- Value-state preservation remains separately governed.
- Future implementation must refuse rather than guess unresolved authority.

## Dependencies and deferred boundaries

- [Issue #6](https://github.com/ThresholdOps/MotiveForce/issues/6): technical analyst identity representation; open and not started.
- [Issue #8](https://github.com/ThresholdOps/MotiveForce/issues/8): detailed partial-compilation dependency closure; open and not started.
- [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20): mapping-rule and target-profile details; open and not started.
- [Issue #21](https://github.com/ThresholdOps/MotiveForce/issues/21): expanded contract-test matrix; open and not started.
- M2: machine schema and executable validation.

## Related artifacts

- [M1.2.4 contract](../../docs/ANALYST_DECISION_STALENESS_REVALIDATION_CONTRACT.md)
- [M1.2 milestone](../milestones/M1-2-process-ir-machine-readiness.md)
- [M1.2.4 milestone](../milestones/M1-2-4-analyst-decision-staleness-revalidation.md)
- [REV-0009](../reviews/M1-2-4-analyst-decision-staleness-revalidation-review.md)
- [REV-0010](../reviews/M1-2-4-analyst-decision-staleness-revalidation-review-2.md)
- [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19)

## Human review round 1

[REV-0009](../reviews/M1-2-4-analyst-decision-staleness-revalidation-review.md) reviewed source head `74d288fd57810f0b1a2c7865185889f07e67146e` and returned `Request changes`.

The overall architecture is retained. Required corrections are:

- `REV9-FIND-001`: distinguish historical authority from source evidence,
- `REV9-FIND-002`: define exact relevance dispositions and their authority,
- `REV9-FIND-003`: separate derived invalidation from explicit invalidation acts,
- `REV9-FIND-004`: correct diagnostic-to-outcome crosswalk fidelity.

This Request changes outcome remains immutable review provenance.

## Human review round 2

[REV-0010](../reviews/M1-2-4-analyst-decision-staleness-revalidation-review-2.md) reviewed corrected semantic head `4463aafca5e5fa176bcd3bb0db604b0a48943d9b` and returned `Approve`.

The final review:

- closes `REV9-FIND-001` through `REV9-FIND-004`,
- accepts historical/current-authority separation and exact basis closure,
- accepts the four-outcome model and exact relevance dispositions,
- accepts the trigger and non-trigger rules,
- accepts the derived and explicit invalidation boundary,
- accepts human revalidation and exact non-transitive controlled carry-forward,
- accepts effective-status behavior and the unchanged 18-code diagnostic crosswalk,
- accepts `STALE-CHOICE-001` through `STALE-CHOICE-010`.

DEC-0008 is `Accepted`, effective as repository authority through merge of PR #25. The decision authorizes no implementation, algorithm, schema, runtime, persistence, API, or executable validation.

## Supersedes

None.

## Superseded by

None.

## Follow-up actions

- Keep M1.2 as a whole incomplete.
- Keep Issues #6, #8, #20, and #21 open and not started.
- Do not start implementation.
- Reopen semantic review only if a later decision proposes to supersede DEC-0008.

Repository-authoritative acceptance is effective through merge of PR #25. No implementation authorization is included.
