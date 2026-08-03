# Milestone Records

Milestone records describe project milestones, scope, acceptance basis, outcomes, and follow-up.

Each milestone record must include:

- milestone ID,
- title,
- status,
- objective,
- scope,
- explicit non-goals,
- deliverables,
- acceptance basis,
- related PRs,
- related commits,
- decisions created,
- outcome,
- follow-up.

Milestone status must reflect repository evidence. Draft milestone content remains proposed until merged.

A milestone record introduced by a PR may record the PR number, branch, reviewed source head, base where material, and expected status transition on merge. It must not predict the PR's future squash merge SHA.

## Current records

- [M0: Concept Definition](M0-concept-definition.md)
- [M1: Process IR Contract](M1-process-ir-contract.md)
- [M1.1: Project Memory Foundation](M1-1-project-memory-foundation.md)
- [M1.2: Process IR Machine-Readiness Hardening](M1-2-process-ir-machine-readiness.md)
- [M1.2.1: RecordEnvelope and Revision Semantics Contract](M1-2-1-record-envelope-revision-semantics.md)
- [M1.2.2: Deterministic Semantic Compiler Replay Contract](M1-2-2-deterministic-semantic-compiler-replay.md), Accepted / Completed through merge of PR #23.
- [M1.2.3: Process IR Diagnostic Severity and Aggregation Policy](M1-2-3-diagnostic-severity-aggregation.md), Accepted / Completed through merge of PR #24.
- [M1.2.4: AnalystDecision Staleness, Invalidation, Revalidation, and Controlled Authority Carry-Forward](M1-2-4-analyst-decision-staleness-revalidation.md), Accepted / Completed through merge of PR #25.
- [M1.2.5: Mapping Rule References, Ruleset Versioning, and Target BPMN Profile Propagation](M1-2-5-mapping-rule-target-profile-propagation.md), Accepted / Completed as design-contract work through merge of PR #26; REV-0013 closes both REV-0012 findings.
- [M1.2.6: Structured Elicitation Extraction](M1-2-6-structured-elicitation-extraction.md), Proposed / In progress for semantic-design work only; Issue #28 is a separate governance gate before REV-0014.
- [M2: Machine Schema and Contract Validation](M2-machine-schema-contract-validation.md)
