# M1.1: Project Memory Foundation

- Milestone ID: `M1.1`
- Title: Project Memory Foundation
- Status: Completed

## Objective

Create a durable, reviewable, repository-native project memory for MøtiveFōrce governance.

## Scope

- `project-memory/` directory and governance records.
- Source-of-truth hierarchy.
- Decision, milestone, review, changelog, glossary, and open-item records.
- GitHub Issue governance for actionable future and deferred work.
- M1 provenance synchronization and REV-0001 provenance correction.
- `memory_schema_version: 1`.

## Explicit non-goals

- No runtime memory.
- No vector database.
- No knowledge graph implementation.
- No application code.
- No machine schema.
- No Process IR implementation.

## Deliverables

- Repository-native project memory under `project-memory/`.
- Accepted [DEC-0004](../decisions/DEC-0004-project-memory-governance.md).
- Issue registry in [OPEN_ITEMS.md](../OPEN_ITEMS.md).
- M1 review provenance record in [REV-0001](../reviews/M1-process-ir-semantic-review.md).

## Acceptance basis

M1.1 is completed by merge of [PR #3](https://github.com/ThresholdOps/MotiveForce/pull/3). Before that merge, the PR content was Draft and non-authoritative.

The reviewed PR #3 source head before the final governance amendment was [`24ae8c7ed0487148de2c19a135e7033a03fcad55`](https://github.com/ThresholdOps/MotiveForce/commit/24ae8c7ed0487148de2c19a135e7033a03fcad55). The final source head was [`71343343971c0a867fbade401f26503e87782cc1`](https://github.com/ThresholdOps/MotiveForce/commit/71343343971c0a867fbade401f26503e87782cc1). The PR #3 squash merge commit was [`caff0ba6f33cc0243d78dd61c091968a218a25f8`](https://github.com/ThresholdOps/MotiveForce/commit/caff0ba6f33cc0243d78dd61c091968a218a25f8).

## Related PRs

- [PR #3: M1.1: establish project memory foundation](https://github.com/ThresholdOps/MotiveForce/pull/3)

## Related Issues

- [Issue #4](https://github.com/ThresholdOps/MotiveForce/issues/4) through [Issue #21](https://github.com/ThresholdOps/MotiveForce/issues/21)

## Related commits

- Original project-memory source head [`19bc7a56cd68ea66310d92c0093178fe414fddac`](https://github.com/ThresholdOps/MotiveForce/commit/19bc7a56cd68ea66310d92c0093178fe414fddac)
- Reviewed project-memory head before final governance amendment [`24ae8c7ed0487148de2c19a135e7033a03fcad55`](https://github.com/ThresholdOps/MotiveForce/commit/24ae8c7ed0487148de2c19a135e7033a03fcad55)
- Final PR #3 source head [`71343343971c0a867fbade401f26503e87782cc1`](https://github.com/ThresholdOps/MotiveForce/commit/71343343971c0a867fbade401f26503e87782cc1)
- PR #3 squash merge commit [`caff0ba6f33cc0243d78dd61c091968a218a25f8`](https://github.com/ThresholdOps/MotiveForce/commit/caff0ba6f33cc0243d78dd61c091968a218a25f8)

## Decisions created

- [DEC-0004](../decisions/DEC-0004-project-memory-governance.md)

## Outcome

Project-memory governance is accepted. Issue governance is accepted. `memory_schema_version: 1` is adopted. Initial decision, milestone, review, history, changelog, glossary, open-item, and template records are established. M1 provenance is synchronized and corrected.

## Follow-up

- Continue M1.2 and M2 as deferred future governance/design work.

## Follow-up Issues

- Existing Issues [#4](https://github.com/ThresholdOps/MotiveForce/issues/4)-[#21](https://github.com/ThresholdOps/MotiveForce/issues/21) track future and deferred work. No new Issue is required solely to record PR #3's own merge SHA.
