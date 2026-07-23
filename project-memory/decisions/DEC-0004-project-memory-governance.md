# DEC-0004: Project Memory Governance

- ID: `DEC-0004`
- Title: Repository-native project memory governance
- Status: Accepted
- Date: 2026-07-22T20:08:51Z
- Decision authority: Accepted by merge of [PR #3](https://github.com/ThresholdOps/MotiveForce/pull/3). Before merge, this decision was Proposed in Draft PR #3.

## Context

The project needs durable memory for decisions, milestone history, semantic reviews, open questions, and scope boundaries. This memory must be reviewable and repository-native.

## Decision

`project-memory/` is the project-governance memory layer.

Current state is mutable. History and decisions preserve provenance. Draft work is marked Proposed. No hidden reasoning or confidential material is stored. Changes are linked to repository evidence. Prior records are superseded rather than silently rewritten.

Project memory adopts the source-of-truth hierarchy, decision-versus-implementation status separation, Issue governance, material-change update discipline, minor operational update rule, and self-provenance exception defined in [project-memory/README.md](../README.md).

Governance-affecting changes MUST update project memory in the same PR. Minor operational changes SHOULD update project memory when current state or open work is materially affected; otherwise they MUST link a complete follow-up Issue and record that tracking artifact.

Project memory is the governance index. GitHub Issues are the actionable-work tracker. Deferred and future actionable items require both a project-memory entry and a linked GitHub Issue unless they are already actively tracked by an open PR.

Duplicate Issues must be avoided through open and closed Issue searches before creation. Issues must contain complete context, bounded scope, acceptance criteria, dependencies, related project-memory records, related PRs or commits, risks, and provenance. Project-memory entries must link to the tracking Issue or active PR. Closed, superseded, split, or materially changed Issues must update the project-memory record rather than silently changing provenance.

A project-memory PR must not invent or predict its own future squash merge SHA. It must record its PR number, branch, reviewed source head, base where material, and reviewed state before merge. The final source head after amend and push is recorded in PR metadata. The actual merge SHA remains authoritative in GitHub PR metadata and should be recorded by the next governance-affecting project-memory PR when material.

## Rationale

Git records commits and GitHub records review context, but neither provides a concise governance handoff across milestones. Project memory indexes and summarizes those artifacts without replacing them.

## Alternatives considered

- Store memory only in conversation context: rejected because it is not durable repository state.
- Use a runtime knowledge graph now: rejected as out of current scope.
- Rely only on Git history: rejected because Git does not capture interpreted governance state.

## Consequences

- Governance-affecting PRs must update project memory in the same PR.
- Minor operational PRs should update project memory when materially affected or link a complete follow-up Issue.
- Current-state summaries must be re-verified.
- Historical corrections should be explicit.
- Future and deferred actionable work must be tracked in both project memory and GitHub Issues unless an open PR is actively delivering it.
- Project memory must distinguish decision status from implementation status.
- Issue state changes must be reflected in project memory; a closed Issue does not automatically mean work is completed.
- Project-memory PRs must not predict their own future squash merge SHA.

## Related artifacts

- [PR #3: M1.1: establish project memory foundation](https://github.com/ThresholdOps/MotiveForce/pull/3)
- Original project-memory commit [`19bc7a56cd68ea66310d92c0093178fe414fddac`](https://github.com/ThresholdOps/MotiveForce/commit/19bc7a56cd68ea66310d92c0093178fe414fddac)
- Reviewed PR #3 source head before final governance amendment [`24ae8c7ed0487148de2c19a135e7033a03fcad55`](https://github.com/ThresholdOps/MotiveForce/commit/24ae8c7ed0487148de2c19a135e7033a03fcad55)
- [Issue #4](https://github.com/ThresholdOps/MotiveForce/issues/4) through [Issue #15](https://github.com/ThresholdOps/MotiveForce/issues/15)
- [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16) through [Issue #21](https://github.com/ThresholdOps/MotiveForce/issues/21)
- [project-memory/README.md](../README.md)
- [project-memory/OPEN_ITEMS.md](../OPEN_ITEMS.md)
- [M1.2 milestone](../milestones/M1-2-process-ir-machine-readiness.md)
- [M2 milestone](../milestones/M2-machine-schema-contract-validation.md)

## Supersedes

None.

## Superseded by

None.

## Follow-up actions

- Record the PR #3 squash merge commit in the next governance-affecting project-memory PR if material.
- Continue checking Issue links during governance-affecting updates.
