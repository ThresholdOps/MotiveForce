# Structured Elicitation Extraction Contract

- Project: MøtiveFōrce
- Milestone: `M1.2.6`
- Decision: `DEC-0010`
- Status: Proposed
- Scope: exact `SourceArtifact` revision and `EvidenceFragment` revisions to proposed `AtomicStatement` revisions
- Tracking Issue: [Issue #27](https://github.com/ThresholdOps/MotiveForce/issues/27)
- Governance gate: [Issue #28](https://github.com/ThresholdOps/MotiveForce/issues/28)
- Current project status: Concept / pre-MVP

This document is a Proposed semantic design contract. It is not an implementation, machine schema, serialization contract, validator, fixture, evaluation suite, prompt, training artifact, transcription system, or BPMN mapping contract.

## 1. Purpose

This contract defines a bounded elicitation-extraction stage that locates immutable evidence within one exact source revision and derives contestable, proposed atomic business assertions. The stage preserves what a source says and what remains unresolved without deciding accepted business meaning.

The contract reuses accepted Process IR records. It does not create a second source model, a second Process IR, or an alternative authority path.

## 2. Accepted basis

This proposal depends on, and does not amend, the following accepted contracts:

- the M1 Process IR contract for `SourceArtifact`, `EvidenceFragment`, `AtomicStatement`, `CandidateRelation`, `Finding`, `AnalystDecision`, evidence, and authority boundaries;
- the M1.2.1 RecordEnvelope contract for logical identity, exact revisions, immutable evidence, derivation, supersession, and record status;
- the M1.2.3 diagnostic policy for the separation of analytical Findings and Process IR diagnostics;
- the M1.2.4 contract for human authority, current authority, staleness, revalidation, and controlled carry-forward;
- the M1.2.5 contract for downstream mapping, compiler, profile, and Kernel provenance boundaries.

M1.2.6 is upstream of semantic classification and BPMN mapping. Nothing in this contract authorizes either activity.

## 3. Authority boundary

The extraction stage MAY:

- locate exact source evidence;
- segment source content for evidence accounting;
- derive proposed `AtomicStatement` revisions;
- preserve linguistic qualifiers and discourse relationships;
- record non-authoritative extraction observations;
- record a source attestation as additional evidence.

The extraction stage MUST NOT:

- accept, reject, resolve, or normalize business meaning authoritatively;
- infer a process performer from the identity of a speaker;
- select a BPMN concept or create a `ProposedBPMNMapping`;
- create or resolve a `Finding` merely from an extraction observation;
- issue an `AnalystDecision`;
- treat confidence as authority;
- silently complete, smooth, delete, or replace source logic;
- change any output to `accepted`.

An authorized human `AnalystDecision` remains required before source-derived business meaning becomes accepted under M1.

## 4. Exact extraction basis

One extraction run MUST have exactly one request-selected exact `SourceArtifact` revision as its source basis.

Every `EvidenceFragment` considered by that run MUST:

- use the accepted `RecordEnvelope`;
- identify the exact logical source and exact source revision from which it was located;
- preserve the original source wording or source content referenced by the accepted M1 contract;
- remain immutable;
- have an addressable location within the exact source revision;
- preserve source-order information sufficient to distinguish repeated content when ordering is available.

A new or corrected transcript, workshop note, interview response, process-owner statement, or other source is a new `SourceArtifact` revision or a new logical `SourceArtifact` as required by accepted identity rules. Extraction MUST NOT rewrite an existing evidence revision to reflect a later correction.

The location mechanism, character-unit convention, normalization algorithm, serialization, digest, and canonicalization rules are deferred. Their absence does not permit an ambiguous or non-unique evidence location to be presented as exact.

## 5. Evidence coverage

The extraction stage MUST account for the complete assessable content boundary of the exact source revision.

Each assessable source region MUST be accounted for as one of:

- assertion-bearing evidence referenced by one or more proposed `AtomicStatement` revisions;
- non-assertive content with an explicit bounded rationale;
- content whose extraction assessment could not be completed, with an `ExtractionValidationObservation`;
- content explicitly outside the assessable source boundary under a stated source-boundary rule.

`irrelevant` is not a permitted disposition for hiding business assertions, side processes, variants, exceptions, corrections, or inconvenient evidence. A source region MAY be classified as non-assertive only when it does not itself assert contestable business meaning. Greetings, transcription markers, incomplete fillers without recoverable assertions, and purely conversational navigation MAY be non-assertive; the rationale MUST remain auditable.

Coverage is an extraction-completeness claim only. It is not a claim that the described business process is complete, correct, current, or internally consistent.

## 6. Atomic statement derivation

Each derived `AtomicStatement` MUST:

- use the accepted `RecordEnvelope`;
- remain `proposed`;
- represent one indivisible, contestable, source-derived business assertion;
- reference one or more exact `EvidenceFragment` revisions sufficient to support the assertion;
- preserve derivation from the exact source basis;
- preserve source wording separately from any bounded restatement;
- preserve negation, conditions, modality, uncertainty, frequency, quantity, and other material qualifiers;
- identify the speaker only as provenance when the source supplies a speaker;
- leave an actor or performer unresolved when the source does not establish one.

One sentence MAY produce multiple `AtomicStatement` revisions. Multiple sentences MAY support one atomic assertion only when the resulting statement still expresses one contestable claim and all supporting evidence remains explicit. The extraction stage MUST NOT combine distinct alternatives, actors, conditions, outcomes, or temporal claims into one statement merely to make the account smoother.

An `AtomicStatement` is not accepted business meaning, a process step, an actor assignment, a `Finding`, or a BPMN object.

## 7. Linguistic fidelity

The extraction stage MUST preserve distinctions that can change business meaning, including:

- asserted versus negated;
- always versus usually, sometimes, rarely, or conditionally;
- required versus permitted, preferred, possible, or uncertain;
- singular versus plural and bounded versus unbounded quantity where stated;
- current practice versus historical, planned, hypothetical, or recalled practice;
- direct assertion versus hearsay, assumption, question, or reported policy;
- named subject versus omitted, passive, ambiguous, or collective subject.

The stage MAY flag such distinctions for later interpretation. It MUST NOT resolve them by defaulting to the most convenient process flow.

## 8. Speaker and performer

Speaker provenance answers who supplied the words. It never answers who performs the described business activity.

A statement such as “the request is registered” spoken by person `W` MAY record `W` as the speaker when supported by source metadata. It MUST NOT record `W` as the performer unless the source separately supports that responsibility.

An absent, passive, ambiguous, or collective grammatical subject is an extraction observation or preserved linguistic property. Whether it becomes a process-level missing-actor Finding belongs to a later analytical stage.

## 9. Corrections and potential contradictions

Later source content MUST NOT destructively replace an earlier source-derived statement.

When the source explicitly corrects an earlier assertion:

- both proposed `AtomicStatement` revisions remain preserved;
- the correcting statement MUST explicitly reference the corrected statement through a `corrects` relation;
- the relation points from the correcting statement to the earlier corrected statement;
- the relation is non-authoritative and does not delete evidence or by itself choose accepted business meaning.

When two preserved assertions may conflict but the source does not explicitly perform a correction, extraction MAY record a `potentially contradicts` relation. That relation:

- is a signal for later analysis, not a `Finding`;
- preserves both assertions and their exact evidence;
- MUST NOT contain a selected winner;
- is semantically symmetric, while an eventual machine representation MAY use a deterministic storage direction defined by a later serialization contract.

A return to an earlier position does not erase intervening statements. Any future `reaffirms` relation is outside this contract unless separately proposed and reviewed.

## 10. ExtractionValidationObservation

This proposal adopts `ExtractionValidationObservation` as a new non-authoritative conceptual record because extraction defects must be preserved without prematurely creating a process-semantic `Finding` or a Process IR diagnostic.

An `ExtractionValidationObservation` MUST:

- use the accepted `RecordEnvelope`;
- reference the exact extraction basis and affected exact record revisions or source locations;
- describe one bounded extraction condition;
- preserve supporting evidence and rationale;
- remain non-authoritative and never become `accepted` business meaning;
- be superseded rather than silently rewritten when the observation changes;
- state whether extraction output is complete, partial, or blocked for its affected scope without claiming process completeness.

Observation categories MAY include:

- ambiguous or absent grammatical subject;
- missing, invalid, ambiguous, or non-unique evidence location;
- incomplete source-assertion coverage;
- suspected speaker-to-performer inference;
- invalid or unresolved correction reference;
- loss of a material linguistic qualifier;
- suspected silent deletion, replacement, or smoothing;
- incomplete extraction assessment.

These category names are conceptual and are not diagnostic codes.

The following separation is normative:

`ExtractionValidationObservation` ≠ `Finding` ≠ Process IR diagnostic ≠ `AnalystDecision`.

An observation MAY be referenced by a later analytical record. It MUST NOT automatically promote itself into a `Finding`, resolve a `Finding`, emit a Process IR diagnostic, or grant decision authority. M2 MAY define its machine representation and validation mapping only after this semantic contract is accepted; it MUST preserve these authority boundaries and MUST NOT create a parallel diagnostic registry.

## 11. Source attestation

Source attestation is evidence that an identified source person confirms that the record accurately captures what that person said or what that person reports doing.

Source attestation:

- MUST reference the exact source, evidence, statement, or bounded set of exact revisions being attested;
- MAY improve the provenance quality of that source account;
- MUST preserve the attesting person's identity or approved anonymized identity reference under applicable policy;
- MUST NOT accept business meaning;
- MUST NOT resolve contradictions between sources;
- MUST NOT create an `AnalystDecision`;
- MUST NOT grant authority to compile or map to BPMN.

Two conflicting attested accounts remain two supported accounts requiring later analysis. Attestation is confirmation of testimony, not analytical adjudication.

## 12. Privacy and public-repository safety

Real transcripts, recordings, personal identifiers, confidential procedure content, and source evidence MUST NOT be committed to the public repository under this milestone.

The conceptual contract MAY require speaker provenance, anonymization state, or an approved identity reference. It does not define identity storage, IAM, signatures, consent management, retention, transcription, or anonymization implementation. Those mechanisms require separate policy and implementation authority.

## 13. Boundary to later stages

The output of extraction is evidence and proposed atomic assertions. A later analytical stage may:

- classify business concepts;
- create candidate entities and candidate relations;
- create process-level Findings and unresolved questions;
- propose BPMN mappings only within accepted downstream authority;
- request or record an authorized `AnalystDecision`.

The later stage MUST retain exact evidence and extraction derivation. It MUST NOT treat extraction coverage, an extraction observation, a correction relation, potential contradiction, confidence, or source attestation as accepted business meaning.

## 14. Lifecycle and replay implications

Exact source, evidence, statement, relation, observation, and attestation revisions form the extraction basis for any later analytical work that claims reproducibility.

If an exact source revision changes, a later run is a changed basis. Statements and observations derived from the earlier source remain historical records. They are not silently re-pointed to the new source.

This contract does not define an executable extraction manifest, replay algorithm, digest algorithm, or comparison projection. M2 may define those artifacts only while preserving exact revision and derivation semantics.

## 15. Non-goals

M1.2.6 does not define or create:

- JSON Schema or another machine schema;
- serialization, field casing, canonicalization, identifier generation, digest, or SHA algorithms;
- executable validation, rulesets, fixtures, evaluations, tests, or CI;
- an agent prompt, training corpus, fine-tuning plan, or runtime agent;
- recording, transcription, diarization, or editing tools;
- a Process Workbench UI;
- draw.io / diagrams.net artifacts;
- BPMN mapping rules or BPMN object selection;
- Process IR diagnostic codes or changes to the accepted registry;
- Finding resolution, AnalystDecision authority, compiler behavior, or Kernel validation;
- identity, privacy, consent, retention, signature, or attestation implementation;
- confidential or personal source content in this repository.

## 16. Governance gate

[Issue #28](https://github.com/ThresholdOps/MotiveForce/issues/28) tracks merge-strategy governance separately from this semantic contract.

That Issue MUST be consciously started and resolved before a `REV-0014` evidence package is frozen or REV-0014 begins, whichever occurs first. While it remains unresolved, REV-0014 MUST NOT record `Approve`, grant merge authorization, or authorize bounded finalization.

This contract does not choose a merge strategy and does not decide whether the eventual governance result amends DEC-0004 or creates another decision.

## 17. Acceptance criteria

Human semantic review must determine whether:

- accepted source, evidence, statement, envelope, Finding, diagnostic, and decision concepts are reused without a competing model;
- every proposed statement carries exact evidence and one contestable assertion;
- evidence coverage is auditable without an `irrelevant` suppression channel;
- non-assertive content is bounded without token-level atomization;
- linguistic qualifiers, corrections, and potential contradictions are preserved;
- speaker provenance cannot become performer responsibility by inference;
- source attestation cannot become semantic acceptance;
- `ExtractionValidationObservation` has a necessary, bounded, non-authoritative role and an explicit M2 path;
- the extraction stage cannot perform BPMN mapping or accepted semantic interpretation;
- schema, fixtures, implementation, prompts, and executable validation remain deferred.

Until a separate human review accepts the design, this contract, DEC-0010, and M1.2.6 remain Proposed.

## 18. Related artifacts

- [Issue #27](https://github.com/ThresholdOps/MotiveForce/issues/27)
- [Issue #28](https://github.com/ThresholdOps/MotiveForce/issues/28)
- [DEC-0010](../project-memory/decisions/DEC-0010-structured-elicitation-extraction.md)
- [M1.2.6 milestone](../project-memory/milestones/M1-2-6-structured-elicitation-extraction.md)
- [M1 Process IR contract](PROCESS_IR_CONTRACT.md)
- [M1.2.1 RecordEnvelope contract](PROCESS_IR_RECORD_ENVELOPE_CONTRACT.md)
- [M1.2.3 diagnostic policy](PROCESS_IR_DIAGNOSTIC_POLICY_CONTRACT.md)
- [M1.2.4 staleness and revalidation contract](ANALYST_DECISION_STALENESS_REVALIDATION_CONTRACT.md)
- [M1.2.5 mapping and target-profile contract](MAPPING_RULE_TARGET_PROFILE_PROPAGATION_CONTRACT.md)
