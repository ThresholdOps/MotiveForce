# Current State

- Last verified: 2026-08-03T11:29:08Z
- Verification source: fetched GitHub `main` and direct remote-head query at [`d0bf81770179883441389603a34915cb1bb2890b`](https://github.com/ThresholdOps/MotiveForce/commit/d0bf81770179883441389603a34915cb1bb2890b); merged [PR #30](https://github.com/ThresholdOps/MotiveForce/pull/30); closed [Issue #28](https://github.com/ThresholdOps/MotiveForce/issues/28); active Draft PR #29; and project-memory ID registries across `main` and PR #29.
- Active branch: `design/m1-2-6-structured-elicitation-extraction`, rebased exactly onto `d0bf81770179883441389603a34915cb1bb2890b`. Its synchronized source head remains authoritative in PR #29 metadata after push.

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

## Completed merge-strategy governance

- [Issue #28](https://github.com/ThresholdOps/MotiveForce/issues/28), `OPEN-0021`, is closed as completed.
- [DEC-0011](decisions/DEC-0011-reviewed-finalization-merge-strategy.md) is Accepted through merge of [PR #30](https://github.com/ThresholdOps/MotiveForce/pull/30).
- PR #30 reviewed head `e0020a44b0b649b711402d282d4cf5ece31708a8`, finalization head `a5304a5e5c2c122d5b8dedfcd864c5f6c4429999`, and merge commit [`d0bf81770179883441389603a34915cb1bb2890b`](https://github.com/ThresholdOps/MotiveForce/commit/d0bf81770179883441389603a34915cb1bb2890b) retain the exact governance provenance.
- The Issue #28 gate is satisfied. DEC-0011 applies to REV-0014 and later covered reviews; no REV-0014 record is created by this synchronization.

## Deferred work

Issues [#4](https://github.com/ThresholdOps/MotiveForce/issues/4)-[#15](https://github.com/ThresholdOps/MotiveForce/issues/15) and [#21](https://github.com/ThresholdOps/MotiveForce/issues/21) remain open and deferred or future work. M1.2 remains incomplete at the design-program level.

## Current blockers and gates

- No blocker prevents drafting the Proposed M1.2.6 semantic contract.
- The Issue #28 governance gate is resolved and no longer blocks REV-0014.
- Human semantic review remains required before DEC-0010, the contract, or M1.2.6 can become Accepted.

## Next expected action

Conduct the separate human semantic and design review against the exact synchronized PR #29 head. Do not treat this base-and-gate synchronization as semantic acceptance.

## Current out-of-scope areas

- production application or runtime agent;
- BPMN Kernel or Semantic Compiler implementation;
- machine-readable schema, canonicalization, identifiers, digests, or serialization;
- executable validator, ruleset, fixture, evaluation, test, or CI;
- prompts, training, fine-tuning, or transcription tooling;
- Process Workbench UI or draw.io adapter work;
- BPMN mapping during elicitation extraction;
- confidential source documents or personal data in the public repository;
- any change to accepted DEC-0011 merge-strategy governance within the M1.2.6 semantic proposal.
