# Scope

## Current product scope

Current product scope is conceptual and pre-MVP:

- semantic analysis of unstructured process documentation and structured elicitation sources;
- evidence-backed canonical semantic model;
- explicit uncertainty and contradiction handling;
- Process IR boundary between Analytical Agent and Semantic Compiler;
- future deterministic BPMN 2.0.2 compilation and validation;
- future export projections.

## Current milestone scope

Completed milestones and design increments:

- M1 Process IR contract, accepted through [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2).
- M1.1 Project Memory Foundation, accepted through [PR #3](https://github.com/ThresholdOps/MotiveForce/pull/3).
- M1.2.1 through M1.2.5 design-contract work, accepted through PRs [#22](https://github.com/ThresholdOps/MotiveForce/pull/22)-[#26](https://github.com/ThresholdOps/MotiveForce/pull/26).
- M1.2.5 is represented on `main` by PR #26 squash merge [`2387307f2f7a3f05b65197497b9f0945bb26bf6a`](https://github.com/ThresholdOps/MotiveForce/commit/2387307f2f7a3f05b65197497b9f0945bb26bf6a); Issue #20 is closed after human attestation.

Active proposed design increment:

- M1.2.6 Structured Elicitation Extraction, tracked by [Issue #27](https://github.com/ThresholdOps/MotiveForce/issues/27), defines the semantic input boundary from one exact `SourceArtifact` revision and immutable `EvidenceFragment` revisions to proposed `AtomicStatement` revisions.
- The [M1.2.6 contract](../docs/STRUCTURED_ELICITATION_EXTRACTION_CONTRACT.md), [DEC-0010](decisions/DEC-0010-structured-elicitation-extraction.md), and [M1.2.6 milestone](milestones/M1-2-6-structured-elicitation-extraction.md) are Proposed.
- `ExtractionValidationObservation` is proposed as a non-authoritative extraction record distinct from Finding, Process IR diagnostic, and AnalystDecision.
- Work is limited to semantic documentation and project governance. No human acceptance is claimed.

Separate governance scope:

- [Issue #28](https://github.com/ThresholdOps/MotiveForce/issues/28) tracks merge-strategy governance as `Open / Not started` under `OPEN-0021`.
- It must resolve before REV-0014 begins or its evidence package is frozen.
- It does not reopen PR #26, change M1.2.5 acceptance, resolve merge strategy in this PR, or yet decide DEC-0004 amendment versus a new decision.

Future milestone:

- M2 Machine Schema and Contract Validation remains future work after accepted semantic contracts; implementation is deferred.

## M1.2.6 in scope

- exact one-source-revision extraction basis;
- immutable, addressable evidence fragments;
- one contestable source-derived assertion per proposed atomic statement;
- auditable source-content coverage and explicit non-assertive treatment;
- preservation of negation, conditions, modality, uncertainty, frequency, and quantity;
- speaker provenance without performer inference;
- non-destructive correction and potential-contradiction relations;
- bounded extraction observations and their M2 boundary;
- source attestation as testimony confirmation, never semantic acceptance;
- privacy, anonymization, and public-repository constraints;
- later semantic-analysis and BPMN-mapping boundary.

## Explicit non-goals for M1.2.6

- no JSON Schema or machine schema;
- no serialization, casing, canonicalization, identifier, digest, or SHA algorithm;
- no executable validator, ruleset, fixture, evaluation, test, or CI;
- no prompt, agent training, fine-tuning, runtime agent, or transcription tooling;
- no Process Workbench UI or draw.io work;
- no BPMN mapping, compiler, Kernel, or process-model implementation;
- no changes to accepted diagnostic codes;
- no confidential sources or personal data;
- no Accepted status, REV-0014, or merge-strategy decision during conscious start.

## Future scope

Future, not yet committed as implementation:

- Process Workbench;
- Analytical Agent;
- Semantic Compiler;
- deterministic BPMN 2.0.2 Kernel;
- BPMN XML and BPMN DI projections;
- draw.io or diagrams.net export;
- Process registers, RACI, evidence, and findings reports;
- machine schema and staged extraction evaluation;
- cross-process knowledge graph governance.

## Decision and implementation status

Decision status and implementation status are independent. Proposed semantic documents do not authorize runtime implementation.

| Item | Decision status | Implementation status | Tracking |
| --- | --- | --- | --- |
| M1 Process IR contract | Accepted | Design complete; runtime not started | [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2) |
| M1.2.1-M1.2.5 | Accepted | Design-contract work completed; runtime not started | PRs [#22](https://github.com/ThresholdOps/MotiveForce/pull/22)-[#26](https://github.com/ThresholdOps/MotiveForce/pull/26) |
| M1.2.6 structured elicitation extraction | Proposed | In progress for semantic design only | [Issue #27](https://github.com/ThresholdOps/MotiveForce/issues/27), [DEC-0010](decisions/DEC-0010-structured-elicitation-extraction.md) |
| Merge-strategy governance | Open | Not started | [Issue #28](https://github.com/ThresholdOps/MotiveForce/issues/28) |
| M2 machine schema and contract validation | Open / Proposed milestone | Deferred | [Issue #5](https://github.com/ThresholdOps/MotiveForce/issues/5), [M2](milestones/M2-machine-schema-contract-validation.md) |
