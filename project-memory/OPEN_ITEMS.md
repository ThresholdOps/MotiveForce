# Open Items

This file tracks open decisions, semantic review questions, risks, assumptions, and next actions.

Decision status and implementation status are independent:

- Decision status: `Open`, `Proposed`, `Accepted`, `Rejected`, or `Deferred`.
- Implementation status: `Not started`, `Deferred in current phase`, `In progress`, `Blocked`, `Completed`, or `Not applicable`.

A decision may be `Open` while implementation is `Deferred in current phase`. Deferred implementation does not mean the decision has been made. `Deferred` as a decision status means the decision itself has intentionally been postponed.

## Issue registry

Every actionable future or deferred item must have a GitHub Issue unless it is already actively tracked by an open PR. No current open item uses the PR #2 active-PR exception because PR #2 has merged.

| Item ID | Title | Category | Decision status | Implementation status | Tracking artifact | Related decision or milestone | Dependency | Next review point |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `OPEN-0001` | Process IR contract | Semantic contract | Accepted | Completed | Merged [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2). No Issue required because the milestone is complete. | [M1](milestones/M1-process-ir-contract.md), [DEC-0002](decisions/DEC-0002-agent-compiler-kernel-authority.md), [DEC-0003](decisions/DEC-0003-process-ir-before-kernel.md) | None. | No further review unless a future decision supersedes M1. |
| `OPEN-0002` | Final Process IR validation path | Decision | Open | Deferred in current phase | [Issue #4](https://github.com/ThresholdOps/MotiveForce/issues/4) | [M1](milestones/M1-process-ir-contract.md) | M1 acceptance is satisfied. | Decide next validation path. |
| `OPEN-0003` | Machine-readable Process IR schema contract | Design | Open | Deferred in current phase | Reused [Issue #5](https://github.com/ThresholdOps/MotiveForce/issues/5) | [M2](milestones/M2-machine-schema-contract-validation.md), [DEC-0003](decisions/DEC-0003-process-ir-before-kernel.md) | M1 acceptance is satisfied; M1.2 decisions remain. | After M1.2 hardening decisions. |
| `OPEN-0004` | Analyst identity representation | Decision | Open | Deferred in current phase | [Issue #6](https://github.com/ThresholdOps/MotiveForce/issues/6) | [M1](milestones/M1-process-ir-contract.md) | Accepted M1 authority model. | Before implementing authenticated AnalystDecision workflows. |
| `OPEN-0005` | Confidence calibration | Design | Open | Deferred in current phase | [Issue #7](https://github.com/ThresholdOps/MotiveForce/issues/7) | [REV-0001](reviews/M1-process-ir-semantic-review.md) | Reference-scenario evidence; M1 acceptance is satisfied. | After reference-scenario evidence. |
| `OPEN-0006` | Detailed partial-compilation dependency policy | Design | Open | Deferred in current phase | [Issue #8](https://github.com/ThresholdOps/MotiveForce/issues/8) | [M1.2](milestones/M1-2-process-ir-machine-readiness.md) | Final M1 partial-compilation defaults and scope-register semantics. | Before Semantic Compiler implementation design. |
| `OPEN-0007` | BPMN metamodel-generation strategy | Design | Open | Deferred in current phase | [Issue #9](https://github.com/ThresholdOps/MotiveForce/issues/9) | [DEC-0001](decisions/DEC-0001-canonical-semantic-model.md) | M1 and M2 boundary decisions. | Before BPMN Kernel implementation. |
| `OPEN-0008` | Rule-engine technology | Decision | Open | Deferred in current phase | [Issue #10](https://github.com/ThresholdOps/MotiveForce/issues/10) | [M1](milestones/M1-process-ir-contract.md) | BPMN validation and diagnostic model decisions. | Before deterministic rule implementation. |
| `OPEN-0009` | Persistence strategy | Decision | Open | Deferred in current phase | [Issue #11](https://github.com/ThresholdOps/MotiveForce/issues/11) | [M2](milestones/M2-machine-schema-contract-validation.md) | Machine representation direction. | After Process IR machine representation direction. |
| `OPEN-0010` | Transport API strategy | Decision | Open | Deferred in current phase | [Issue #12](https://github.com/ThresholdOps/MotiveForce/issues/12) | [M2](milestones/M2-machine-schema-contract-validation.md) | Machine representation and identity decisions. | After machine representation and identity decisions. |
| `OPEN-0011` | Process Workbench technology | Design | Open | Deferred in current phase | [Issue #13](https://github.com/ThresholdOps/MotiveForce/issues/13) | [DEC-0002](decisions/DEC-0002-agent-compiler-kernel-authority.md) | Review workflow and runtime boundary decisions. | After review workflows and runtime boundaries are clearer. |
| `OPEN-0012` | draw.io / diagrams.net adapter strategy | Design | Open | Deferred in current phase | [Issue #14](https://github.com/ThresholdOps/MotiveForce/issues/14) | [DEC-0001](decisions/DEC-0001-canonical-semantic-model.md) | BPMN DI and rendering-policy boundaries. | After BPMN DI and rendering-policy boundaries are defined. |
| `OPEN-0013` | Knowledge-graph timing and governance | Decision | Open | Deferred in current phase | [Issue #15](https://github.com/ThresholdOps/MotiveForce/issues/15) | [DEC-0001](decisions/DEC-0001-canonical-semantic-model.md) | Canonical model and Process IR validation. | After canonical model and Process IR validation. |
| `OPEN-0014` | Process IR record envelope and revision semantics | Design | Accepted | Completed for design contract; runtime implementation not started | [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16) and merged [PR #22](https://github.com/ThresholdOps/MotiveForce/pull/22) | [M1.2](milestones/M1-2-process-ir-machine-readiness.md), [M1.2.1](milestones/M1-2-1-record-envelope-revision-semantics.md), [DEC-0005](decisions/DEC-0005-record-envelope-revision-semantics.md), [REV-0002](reviews/M1-2-1-record-envelope-semantic-design-review.md), [REV-0003](reviews/M1-2-1-record-envelope-semantic-design-review-2.md), [REV-0004](reviews/M1-2-1-record-envelope-semantic-design-review-3.md) | M1 acceptance is satisfied; M1.2.1 design is accepted; Issue #19 remains not started. | No further review unless a future decision supersedes DEC-0005 or starts implementation. |
| `OPEN-0015` | Deterministic Semantic Compiler replay contract | Design | Open | Deferred in current phase | Created [Issue #17](https://github.com/ThresholdOps/MotiveForce/issues/17) | [M1.2](milestones/M1-2-process-ir-machine-readiness.md) | Record envelope, digest, and mapping-rule decisions. | During M1.2 planning. |
| `OPEN-0016` | Diagnostic severity and aggregation rules | Design | Open | Deferred in current phase | Created [Issue #18](https://github.com/ThresholdOps/MotiveForce/issues/18) | [M1.2](milestones/M1-2-process-ir-machine-readiness.md) | Final M1 diagnostic catalogue. | During M1.2 planning. |
| `OPEN-0017` | AnalystDecision staleness and invalidation rules | Design | Open | Deferred in current phase; design not started | Created [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19) | [M1.2](milestones/M1-2-process-ir-machine-readiness.md) | Issue #19 is non-blocking for M1.2.1 design acceptance and for the design of exact historical/as-of derivation. It is a hard blocker before implementation that derives authoritative current effective status, evaluates AnalystDecision staleness, invalidation or revalidation, or performs controlled authority carry-forward. | During M1.2 planning, before any current-status or carry-forward implementation. |
| `OPEN-0018` | Mapping-rule references and BPMN profile propagation | Design | Open | Deferred in current phase | Created [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20) | [M1.2](milestones/M1-2-process-ir-machine-readiness.md) | Final target BPMN profile treatment. | During M1.2 planning. |
| `OPEN-0019` | Expanded Process IR contract test matrix | Validation | Open | Deferred in current phase | Created [Issue #21](https://github.com/ThresholdOps/MotiveForce/issues/21) | [M1.2](milestones/M1-2-process-ir-machine-readiness.md), [M2](milestones/M2-machine-schema-contract-validation.md) | Accepted M1 semantics and M1.2 machine-readiness decisions. | Before M2 schema validation. |

## Open semantic review questions

These questions were resolved by merged [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2). They remain listed as review provenance, not active open questions.

| Question | Tracking artifact | Reason no separate Issue is required |
| --- | --- | --- |
| Does the M1 Process IR contract enforce the Agent-Compiler boundary without relying only on prose? | Merged [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2) | Resolved by M1 acceptance. |
| Are the known-absence semantics and revised value-state combination rules acceptable? | Merged [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2) | Resolved by M1 acceptance. |
| Is evidence versus modeling-policy diagnostic separation strict enough? | Merged [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2) | Resolved by M1 acceptance. |
| Is `CompilationPolicyContext` correctly limited to semantic compilation policy? | Merged [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2) | Resolved by M1 acceptance. |
| Is `UNRESOLVED_INTERPRETATION` distinct from ambiguity? | Merged [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2) | Resolved by M1 acceptance. |

## Risks

| Risk ID | Risk | Status | Tracking artifact | Mitigation |
| --- | --- | --- | --- | --- |
| `RISK-0001` | Silent invention of missing business logic. | Accepted mitigation in M1; future validation pending | Merged [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2), [Issue #4](https://github.com/ThresholdOps/MotiveForce/issues/4) | Process IR refusal behavior accepted; reference-scenario validation still future work. |
| `RISK-0002` | Confidence being mistaken for authority. | Accepted mitigation in M1; future calibration pending | Merged [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2), [Issue #7](https://github.com/ThresholdOps/MotiveForce/issues/7) | M1 authority rules plus future confidence calibration. |
| `RISK-0003` | Human decisions replacing evidence. | Accepted mitigation in M1 | Merged [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2) | M1 evidence rules require accepted source-derived assertions to trace to evidence. |
| `RISK-0004` | Overlap between Process IR and BPMN Kernel responsibilities. | Accepted mitigation in M1; kernel design pending | Merged [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2), [Issue #9](https://github.com/ThresholdOps/MotiveForce/issues/9) | Explicit Process IR, compiler, and kernel boundaries. |
| `RISK-0005` | Public-repository leakage. | Accepted mitigation in M1.1 | [DEC-0004](decisions/DEC-0004-project-memory-governance.md) and all future Issues | Public-repository constraints in memory and Issue templates. |
| `RISK-0006` | Documentation drift. | Accepted procedural mitigation in M1.1 | [DEC-0004](decisions/DEC-0004-project-memory-governance.md) | Update discipline in [README.md](README.md). This mitigation is procedural only and is not enforced by tooling. |
| `RISK-0007` | Project-memory summaries becoming stale. | Accepted procedural mitigation in M1.1 | [DEC-0004](decisions/DEC-0004-project-memory-governance.md) | Reverification and stale-link governance. This mitigation is procedural only and is not enforced by tooling. |

## Assumptions

| Assumption ID | Assumption | Basis | Status |
| --- | --- | --- | --- |
| `ASM-0001` | `origin/main` at verification time is [`caff0ba6f33cc0243d78dd61c091968a218a25f8`](https://github.com/ThresholdOps/MotiveForce/commit/caff0ba6f33cc0243d78dd61c091968a218a25f8). | Git fetch and PR #3 metadata. | Verified 2026-07-23T13:06:47Z. |
| `ASM-0002` | M0 is merged through [PR #1](https://github.com/ThresholdOps/MotiveForce/pull/1). | PR #1 metadata. | Verified 2026-07-22T20:29:02Z. |
| `ASM-0003` | M1 is merged and Accepted through [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2). | PR #2 metadata and merged document status. | Verified 2026-07-23T08:08:27Z. |
| `ASM-0004` | M1.1 is completed by [PR #3](https://github.com/ThresholdOps/MotiveForce/pull/3). | PR #3 metadata and merged project-memory content. | Verified 2026-07-23T10:56:40Z before merge; authoritative after PR #3 merge. |
| `ASM-0005` | No implementation exists in merged repository content. | Merged [README.md](../README.md). | Verified from repository content. |

## Non-actionable notes

| Note | Tracking artifact | Reason no Issue is required |
| --- | --- | --- |
| Glossary definitions. | [GLOSSARY.md](GLOSSARY.md) | Informational reference; no independent action unless a future PR changes terminology. |
| Historical observations in [HISTORY.md](HISTORY.md). | [HISTORY.md](HISTORY.md) | Historical record; no action unless a correction is required. |
| Completed M0 concept definition. | [PR #1](https://github.com/ThresholdOps/MotiveForce/pull/1) | Completed and merged; no planned reconsideration. |

## Next actions

1. Keep [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19) deferred until AnalystDecision staleness, invalidation, revalidation, or controlled carry-forward work is deliberately started.
2. Resolve [Issue #4](https://github.com/ThresholdOps/MotiveForce/issues/4) after the M1.2.1 acceptance path is merged.
