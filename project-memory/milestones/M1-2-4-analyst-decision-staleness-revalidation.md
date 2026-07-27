# M1.2.4: AnalystDecision Staleness, Invalidation, Revalidation, and Controlled Authority Carry-Forward

- Milestone ID: `M1.2.4`
- Title: AnalystDecision Staleness, Invalidation, Revalidation, and Controlled Authority Carry-Forward Policy
- Decision status: Accepted
- Milestone status: Completed
- Implementation status: Completed for design contract; runtime implementation not started
- Tracking Issue: [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19)
- Source branch: `design/m1-2-4-analyst-decision-staleness`
- Completion PR: [PR #25](https://github.com/ThresholdOps/MotiveForce/pull/25)
- Base `main`: [`006574b25732f0776a7e510fd33838c9946d9677`](https://github.com/ThresholdOps/MotiveForce/commit/006574b25732f0776a7e510fd33838c9946d9677)
- Initial source head: [`377a6019afa65af9953e1f1dbcc8258416d94f50`](https://github.com/ThresholdOps/MotiveForce/commit/377a6019afa65af9953e1f1dbcc8258416d94f50)

## Objective

Define the Accepted policy for historical validity, current authority, staleness, invalidation, human revalidation, and controlled authority carry-forward for exact `AnalystDecision` revisions.

## Scope

- Historical/as-of validity versus current authority.
- Exact `AnalystDecisionBasisSet`.
- Four current-authority outcomes.
- Relevant staleness and invalidation triggers.
- Explicit non-triggers.
- Exact human revalidation and invalidation bases.
- Controlled, non-transitive carry-forward.
- Effective-status and value-state interaction.
- Inherited diagnostic crosswalk.
- Identity, partial-compilation, and replay boundaries.
- Synthetic examples and manual review tests.

## Explicit non-goals

- No schema or programming-language model.
- No staleness, rule, workflow, scheduling, or notification engine.
- No identity implementation, IAM, directory, or personal-data model.
- No runtime logging, API, persistence, database, or UI specification.
- No executable validation, tests, fixtures, or CI.
- No automatic authority agent or automatic carry-forward.
- No start of Issues #6, #8, #20, or #21.

## Deliverables

- Accepted [M1.2.4 contract](../../docs/ANALYST_DECISION_STALENESS_REVALIDATION_CONTRACT.md).
- Accepted [DEC-0008](../decisions/DEC-0008-analyst-decision-staleness-revalidation.md).
- M1.2.4 and project-memory status synchronization.
- Issue #19 and PR #25 provenance.

## Acceptance criteria

Completion requires:

- human semantic and design review,
- accepted historical/current-authority separation,
- accepted exact-basis and four-outcome model,
- accepted staleness, invalidation, revalidation, and carry-forward rules,
- contract status changed to `Accepted`,
- DEC-0008 changed to `Accepted`,
- merge of the delivery PR,
- project-memory synchronization recording the accepted result.

The design-contract criteria are completed through final human review REV-0010 and merge of PR #25. Runtime implementation criteria remain outside this milestone.

## Dependencies

- M1 is Accepted and Completed.
- M1.2.1, M1.2.2, and M1.2.3 are Accepted and Completed.
- Issue #6 remains responsible for technical identity representation.
- Issue #8 remains responsible for detailed partial-compilation dependency closure.
- Issue #20 remains responsible for mapping and target-profile details.
- Issue #21 remains responsible for expanded contract tests.

## Human reviews

Human review round 1 is recorded by [REV-0009](../reviews/M1-2-4-analyst-decision-staleness-revalidation-review.md).

- Reviewed head: `74d288fd57810f0b1a2c7865185889f07e67146e`
- Outcome: `Request changes`
- Overall architecture: retained
- Findings: `REV9-FIND-001` through `REV9-FIND-004`
- Decision effect: no acceptance and no merge authorization
- Round-1 decision effect: the corrected successor required human semantic and design re-review

Final human semantic and design review is recorded by [REV-0010](../reviews/M1-2-4-analyst-decision-staleness-revalidation-review-2.md).

- Reviewed semantic head: `4463aafca5e5fa176bcd3bb0db604b0a48943d9b`
- Outcome: `Approve`
- `REV9-FIND-001` through `REV9-FIND-004`: closed
- Decision effect: contract and DEC-0008 approved; merge authorized after bounded finalization validation
- Completion: repository-authoritative through merge of PR #25
- Implementation effect: none

## Outcome

Accepted and Completed as design-contract work through merge of PR #25. Issue #19 is closed after merge. Runtime implementation, schema, staleness engine, workflow engine, identity implementation, API, persistence, tests, and CI have not started.

The actual squash merge SHA remains authoritative in GitHub metadata and is not predicted in repository content.

## Follow-up

- Keep M1.2 as a whole not completed.
- Keep Issues #6, #8, #20, and #21 open and not started.
- Do not start runtime implementation without a separately authorized delivery.
- Issue #20 may be considered for a later conscious start.
