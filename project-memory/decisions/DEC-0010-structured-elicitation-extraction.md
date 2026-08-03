# DEC-0010: Structured Elicitation Extraction

- ID: `DEC-0010`
- Title: Structured elicitation extraction from exact source evidence to proposed atomic statements
- Status: Proposed
- Date: 2026-08-03
- Decision authority: Proposed in the M1.2.6 Draft PR; a separate human semantic review is required before acceptance.
- Tracking Issue: [Issue #27](https://github.com/ThresholdOps/MotiveForce/issues/27)
- Governance dependency: [Issue #28](https://github.com/ThresholdOps/MotiveForce/issues/28), resolved through accepted [DEC-0011](DEC-0011-reviewed-finalization-merge-strategy.md) and merge of PR #30
- Source branch: `design/m1-2-6-structured-elicitation-extraction`
- Exact base: [`d0bf81770179883441389603a34915cb1bb2890b`](https://github.com/ThresholdOps/MotiveForce/commit/d0bf81770179883441389603a34915cb1bb2890b)

## Context

Accepted M1 already models source artifacts, evidence fragments, atomic statements, Findings, and human AnalystDecisions. Accepted M1.2.1 supplies exact record revision and envelope semantics. The project needs a deliberately smaller input projection for employee interviews, workshops, process-owner statements, and similar elicitation sources without allowing extraction to become hidden business analysis or BPMN modeling.

Without a bounded contract, an extraction agent could combine assertions, erase corrections, infer performers from speakers, convert uncertainty into default flow, suppress side processes as irrelevant, or treat a source person's confirmation as accepted business meaning.

## Proposed decision

Define one extraction stage whose exact basis is one exact `SourceArtifact` revision and whose outputs are immutable `EvidenceFragment` revisions, proposed `AtomicStatement` revisions, explicit discourse relations, coverage accounting, source-attestation evidence, and—where needed—non-authoritative `ExtractionValidationObservation` revisions.

The proposal:

- reuses accepted records and `RecordEnvelope` rather than creating a competing source model;
- requires one contestable source-derived assertion per proposed `AtomicStatement`;
- requires exact evidence and derivation provenance;
- preserves negation, conditions, modality, uncertainty, quantifiers, corrections, and potential contradictions;
- treats speaker identity only as provenance and forbids performer inference without evidence;
- forbids an `irrelevant` disposition from silently suppressing business assertions, side processes, variants, or exceptions;
- distinguishes explicit non-assertive coverage from omitted content;
- adopts `ExtractionValidationObservation` as a bounded conceptual record distinct from `Finding`, Process IR diagnostic, and `AnalystDecision`;
- defines source attestation as confirmation of what a person said or reports doing, never business-semantic acceptance;
- leaves semantic classification, Finding creation, BPMN mapping, acceptance, compiler work, and Kernel validation downstream.

All extraction outputs remain non-authoritative. An authorized human `AnalystDecision` remains necessary for accepted business meaning.

## Rationale

A source transcript is evidence, not a process model. A constrained extraction layer can improve completeness and auditability only if it preserves contested and uncertain material instead of optimizing for a smooth diagram.

`ExtractionValidationObservation` is proposed because extraction defects such as ambiguous evidence location, incomplete coverage, speaker-performer leakage, or destructive correction handling must be visible before process-level analysis. Reusing `Finding` would prematurely classify linguistic and mechanical extraction defects as material analytical issues. Reusing Process IR diagnostics would collide with the accepted compiler-facing registry. The new record therefore has no acceptance or resolution authority and may only be referenced by later analysis.

## Alternatives considered

### Treat the extracted table or sketch as accepted Process IR

Rejected because an operational source can attest to testimony but cannot bypass human analytical authority or resolve contradictions across sources.

### Use only free-form extraction notes

Rejected because unversioned notes would not provide exact evidence, lifecycle, derivation, or reproducibility.

### Reuse `Finding` for every extraction defect

Rejected because ambiguous grammar, evidence-location failure, and incomplete extraction coverage are not automatically process-semantic Findings.

### Reuse Process IR diagnostic codes

Rejected because those codes belong to accepted compiler and replay policy; extraction must not create a parallel or reclassified diagnostic registry.

### Omit a separate observation record

Not selected in this proposal. Metadata alone cannot consistently carry one bounded defect, affected exact revisions, evidence, lifecycle, and stage outcome without overloading accepted semantic records.

### Define schema, fixtures, or a prompt now

Rejected for M1.2.6 because machine representation and evaluation should follow an accepted semantic contract, not define it implicitly.

## Consequences

- Extraction becomes a separately reviewable, non-authoritative stage.
- Every assertion retains exact source evidence and linguistic fidelity.
- Corrections and potential contradictions remain visible rather than averaged.
- A source person's confirmation strengthens testimony provenance but never substitutes for AnalystDecision.
- M2 must decide machine representation and validation while preserving the new observation boundary.
- Later fixture and agent work can be gated per stage, but none is authorized by this decision.
- Public-repository work remains limited to synthetic or non-sensitive design artifacts under separate future authority.
- Merge-strategy governance remains separate and is resolved by accepted DEC-0011; this status synchronization does not change the M1.2.6 semantic proposal.

## Related artifacts

- [Structured Elicitation Extraction Contract](../../docs/STRUCTURED_ELICITATION_EXTRACTION_CONTRACT.md)
- [M1.2.6 milestone](../milestones/M1-2-6-structured-elicitation-extraction.md)
- [M1.2 parent milestone](../milestones/M1-2-process-ir-machine-readiness.md)
- [Issue #27](https://github.com/ThresholdOps/MotiveForce/issues/27)
- [Issue #28](https://github.com/ThresholdOps/MotiveForce/issues/28)
- [DEC-0004](DEC-0004-project-memory-governance.md), unchanged by this proposal
- [M1 Process IR contract](../../docs/PROCESS_IR_CONTRACT.md)
- [M1.2.1 RecordEnvelope contract](../../docs/PROCESS_IR_RECORD_ENVELOPE_CONTRACT.md)

## Supersedes

None.

## Superseded by

None.

## Follow-up actions

- Obtain a separate human semantic and design review against the exact synchronized PR #29 head.
- Apply accepted DEC-0011 to REV-0014; do not treat resolved governance or this synchronization as semantic acceptance.
- If accepted later, route schema and machine-validation work to M2 and Issue #5.
- Keep fixtures, tests, agent prompts, training, transcription, UI, draw.io, and implementation out of M1.2.6.
