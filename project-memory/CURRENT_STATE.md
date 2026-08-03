# Current State

- Last verified: 2026-08-03T10:03:27Z
- Verification source: fetched GitHub `main` and direct remote-head query, both at [`2387307f2f7a3f05b65197497b9f0945bb26bf6a`](https://github.com/ThresholdOps/MotiveForce/commit/2387307f2f7a3f05b65197497b9f0945bb26bf6a); full open-and-closed Issue search; complete project-memory ID-registry search; accepted M1 through M1.2.5 contracts and decisions.
- Active branch: `design/m1-2-6-structured-elicitation-extraction`, based exactly on `2387307f2f7a3f05b65197497b9f0945bb26bf6a`.

## Project status

MøtiveFōrce is `Concept / pre-MVP`.

No application, runtime agent, Semantic Compiler, BPMN Kernel, validator, user interface, export adapter, schema, fixture, or executable test suite is implemented in merged repository content.

## Current architecture thesis

The canonical semantic model is the source of truth. BPMN diagrams, BPMN XML, BPMN DI, draw.io files, tables, RACI matrices, reports, and external-tool formats are projections.

The Analytical Agent interprets source material without accepting business meaning or validating BPMN. The Semantic Compiler maps accepted meaning. The BPMN Kernel validates the resulting BPMN model.

## Completed design milestones

- M0 concept definition: completed through [PR #1](https://github.com/ThresholdOps/MotiveForce/pull/1).
- M1 Process IR contract: accepted and completed through [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2).
- M1.1 Project Memory Foundation: accepted and completed through [PR #3](https://github.com/ThresholdOps/MotiveForce/pull/3).
- M1.2.1 RecordEnvelope and Revision Semantics: accepted and completed through [PR #22](https://github.com/ThresholdOps/MotiveForce/pull/22).
- M1.2.2 Deterministic Semantic Compiler Replay: accepted and completed through [PR #23](https://github.com/ThresholdOps/MotiveForce/pull/23).
- M1.2.3 Diagnostic Severity and Aggregation: accepted and completed through [PR #24](https://github.com/ThresholdOps/MotiveForce/pull/24).
- M1.2.4 AnalystDecision Staleness and Revalidation: accepted and completed through [PR #25](https://github.com/ThresholdOps/MotiveForce/pull/25).
- M1.2.5 Mapping Rule and Target Profile Propagation: accepted and completed through squash merge of [PR #26](https://github.com/ThresholdOps/MotiveForce/pull/26) at [`2387307f2f7a3f05b65197497b9f0945bb26bf6a`](https://github.com/ThresholdOps/MotiveForce/commit/2387307f2f7a3f05b65197497b9f0945bb26bf6a). [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20) is closed after the owner's human attestation. REV-0013 reviewed semantic head `f8d2249e4693305b57bf021c76bdd78b010da24b`; bounded-finalization head was `04d1db644bab4ab0e30973cda57a57d6065ec019`.

## Active narrow design work

M1.2.6 Structured Elicitation Extraction is the only active semantic-design item.

- [Issue #27](https://github.com/ThresholdOps/MotiveForce/issues/27) tracks `OPEN-0020`.
- [DEC-0010](decisions/DEC-0010-structured-elicitation-extraction.md), the [M1.2.6 contract](../docs/STRUCTURED_ELICITATION_EXTRACTION_CONTRACT.md), and the [M1.2.6 milestone](milestones/M1-2-6-structured-elicitation-extraction.md) are Proposed.
- The work is documentation and governance only.
- A separate human semantic and design review is required before any acceptance transition.
- No REV-0014 record exists and none is authorized by conscious start.

## Governance work

- [Issue #28](https://github.com/ThresholdOps/MotiveForce/issues/28) tracks `OPEN-0021`, merge-strategy governance, as `Open / Not started`.
- Issue #28 does not choose a merge strategy and does not yet decide whether the eventual result amends DEC-0004 or creates a new decision.
- Issue #28 must be consciously started and resolved before the REV-0014 evidence package is frozen or REV-0014 begins, whichever occurs first.
- While Issue #28 is unresolved, REV-0014 cannot record `Approve`, grant merge authorization, or authorize bounded finalization.

## Deferred work

Issues [#4](https://github.com/ThresholdOps/MotiveForce/issues/4)-[#15](https://github.com/ThresholdOps/MotiveForce/issues/15) and [#21](https://github.com/ThresholdOps/MotiveForce/issues/21) remain open and deferred or future work. M1.2 remains incomplete at the design-program level.

## Current blockers and gates

- No blocker prevents drafting the Proposed M1.2.6 semantic contract.
- Issue #28 is a governance gate before REV-0014, not a semantic defect in the Proposed contract.
- Human semantic review remains required before DEC-0010, the contract, or M1.2.6 can become Accepted.

## Next expected action

Review the Draft M1.2.6 proposal while keeping Issue #28 separate. Before REV-0014 begins, consciously start and resolve Issue #28 under its own governance authority.

## Current out-of-scope areas

- production application or runtime agent;
- BPMN Kernel or Semantic Compiler implementation;
- machine-readable schema, canonicalization, identifiers, digests, or serialization;
- executable validator, ruleset, fixture, evaluation, test, or CI;
- prompts, training, fine-tuning, or transcription tooling;
- Process Workbench UI or draw.io adapter work;
- BPMN mapping during elicitation extraction;
- confidential source documents or personal data in the public repository;
- merge-strategy resolution within the M1.2.6 semantic proposal.
