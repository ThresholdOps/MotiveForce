# Scope

## Current product scope

Current product scope is conceptual and pre-MVP:

- semantic analysis of unstructured process documentation,
- evidence-backed canonical semantic model,
- explicit uncertainty and contradiction handling,
- Process IR boundary between Analytical Agent and Semantic Compiler,
- future deterministic BPMN 2.0.2 compilation and validation,
- future export projections.

## Current milestone scope

Completed milestone:

- M1 Process IR contract is accepted and merged through [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2).
- M1.1 Project Memory Foundation is completed by merge of [PR #3](https://github.com/ThresholdOps/MotiveForce/pull/3). It establishes repository-native memory under `project-memory/`, GitHub Issue governance for future actionable work, and `memory_schema_version: 1`.

Proposed future milestones:

- M1.2 Process IR Machine-Readiness Hardening is proposed design work for making the accepted Process IR contract ready for machine representation. It has consciously started through M1.2.1 only; implementation remains limited to documentation and governance. M1.2 as a whole is not completed.
- M1.2.1 RecordEnvelope and Revision Semantics Contract is completed as accepted design-contract work through [PR #22](https://github.com/ThresholdOps/MotiveForce/pull/22), [DEC-0005](decisions/DEC-0005-record-envelope-revision-semantics.md), and [REV-0004](reviews/M1-2-1-record-envelope-semantic-design-review-3.md). It does not create code, schema, runtime components, or executable validation.
- M2 Machine Schema and Contract Validation is proposed as future schema and validation work after M1 acceptance and M1.2 decisions; implementation is deferred in the current phase.

## Explicit non-goals for the current phase

- No production application.
- No runtime agent.
- No BPMN Kernel implementation.
- No machine-readable Process IR schema unless later approved.
- No knowledge graph implementation.
- No confidential source documents in the public repository.
- No replacement of Git, GitHub PRs, or merged repository content.

## Future scope

Future, not yet committed as implementation:

- Process Workbench.
- Analytical Agent.
- Semantic Compiler.
- Deterministic BPMN 2.0.2 Kernel.
- BPMN XML and BPMN DI projections.
- draw.io or diagrams.net export.
- Process registers, RACI, evidence, and findings reports.
- Future tool-specific exports.
- Cross-process knowledge graph governance.

## Decision and implementation status

Decision status and implementation status are independent:

- A decision may be `Open` while implementation is `Deferred in current phase`.
- Deferred implementation does not mean the decision has been made.
- `Deferred` as a decision status means the decision itself has intentionally been postponed.

| Item | Decision status | Implementation status | Tracking |
| --- | --- | --- | --- |
| Process IR contract | Accepted | Completed | Merged [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2), [`54d5e81`](https://github.com/ThresholdOps/MotiveForce/commit/54d5e814601788574d13761561867ce5982cc88c) |
| Project-memory governance | Accepted | Completed | [PR #3](https://github.com/ThresholdOps/MotiveForce/pull/3), [`caff0ba`](https://github.com/ThresholdOps/MotiveForce/commit/caff0ba6f33cc0243d78dd61c091968a218a25f8), [DEC-0004](decisions/DEC-0004-project-memory-governance.md) |
| Final Process IR validation path | Open | Deferred in current phase | [Issue #4](https://github.com/ThresholdOps/MotiveForce/issues/4); M1 acceptance dependency is satisfied |
| Machine-readable Process IR schema contract | Open | Deferred in current phase | [Issue #5](https://github.com/ThresholdOps/MotiveForce/issues/5), [M2](milestones/M2-machine-schema-contract-validation.md) |
| Analyst identity representation | Open | Deferred in current phase | [Issue #6](https://github.com/ThresholdOps/MotiveForce/issues/6) |
| Confidence calibration | Open | Deferred in current phase | [Issue #7](https://github.com/ThresholdOps/MotiveForce/issues/7) |
| Detailed partial-compilation dependency policy | Open | Deferred in current phase | [Issue #8](https://github.com/ThresholdOps/MotiveForce/issues/8) |
| BPMN metamodel-generation strategy | Open | Deferred in current phase | [Issue #9](https://github.com/ThresholdOps/MotiveForce/issues/9) |
| Rule-engine technology | Open | Deferred in current phase | [Issue #10](https://github.com/ThresholdOps/MotiveForce/issues/10) |
| Persistence model | Open | Deferred in current phase | [Issue #11](https://github.com/ThresholdOps/MotiveForce/issues/11) |
| Transport API | Open | Deferred in current phase | [Issue #12](https://github.com/ThresholdOps/MotiveForce/issues/12) |
| Process Workbench technology | Open | Deferred in current phase | [Issue #13](https://github.com/ThresholdOps/MotiveForce/issues/13) |
| draw.io / diagrams.net adapter strategy | Open | Deferred in current phase | [Issue #14](https://github.com/ThresholdOps/MotiveForce/issues/14) |
| Knowledge-graph timing and governance | Open | Deferred in current phase | [Issue #15](https://github.com/ThresholdOps/MotiveForce/issues/15) |
| Process IR record envelope and revision semantics | Accepted | Completed for design contract; runtime implementation not started | [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16), [PR #22](https://github.com/ThresholdOps/MotiveForce/pull/22), [M1.2](milestones/M1-2-process-ir-machine-readiness.md), [M1.2.1](milestones/M1-2-1-record-envelope-revision-semantics.md), [DEC-0005](decisions/DEC-0005-record-envelope-revision-semantics.md) |
| Deterministic Semantic Compiler replay contract | Open | Deferred in current phase | [Issue #17](https://github.com/ThresholdOps/MotiveForce/issues/17), [M1.2](milestones/M1-2-process-ir-machine-readiness.md) |
| Diagnostic severity and aggregation rules | Open | Deferred in current phase | [Issue #18](https://github.com/ThresholdOps/MotiveForce/issues/18), [M1.2](milestones/M1-2-process-ir-machine-readiness.md) |
| AnalystDecision staleness and invalidation rules | Open | Deferred in current phase; design not started | [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19), [M1.2](milestones/M1-2-process-ir-machine-readiness.md). Non-blocking for M1.2.1 design acceptance and exact historical/as-of derivation design; hard blocker before implementation of authoritative current effective-status derivation, AnalystDecision staleness/invalidation/revalidation, or controlled authority carry-forward. |
| Mapping-rule references and BPMN profile propagation | Open | Deferred in current phase | [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20), [M1.2](milestones/M1-2-process-ir-machine-readiness.md) |
| Expanded Process IR contract test matrix | Open | Deferred in current phase | [Issue #21](https://github.com/ThresholdOps/MotiveForce/issues/21), [M1.2](milestones/M1-2-process-ir-machine-readiness.md) |

## Rejected

No product capability has been rejected in merged repository content. Rejected alternatives inside decision records apply only to the decision context in which they are recorded.
