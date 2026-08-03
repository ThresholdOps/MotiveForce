# M1.2.6: Structured Elicitation Extraction

- Milestone ID: `M1.2.6`
- Title: Structured Elicitation Extraction from Source Evidence to Atomic Statements
- Decision status: Proposed
- Milestone status: Proposed
- Implementation status: In progress for semantic-design work only
- Tracking Issue: [Issue #27](https://github.com/ThresholdOps/MotiveForce/issues/27)
- Governance gate: [Issue #28](https://github.com/ThresholdOps/MotiveForce/issues/28), resolved through accepted [DEC-0011](../decisions/DEC-0011-reviewed-finalization-merge-strategy.md) and merge of PR #30
- Active branch: `design/m1-2-6-structured-elicitation-extraction`
- Exact base: [`d0bf81770179883441389603a34915cb1bb2890b`](https://github.com/ThresholdOps/MotiveForce/commit/d0bf81770179883441389603a34915cb1bb2890b)
- Delivery PR: [PR #29](https://github.com/ThresholdOps/MotiveForce/pull/29)
- Human semantic and design review: Required; no review record is created by conscious start

## Objective

Define a Proposed semantic contract for deriving evidence-backed, proposed `AtomicStatement` revisions from one exact `SourceArtifact` revision and its immutable `EvidenceFragment` revisions without granting extraction any business-semantic, acceptance, BPMN, compiler, or Kernel authority.

## Scope

- exact one-source-revision extraction basis;
- immutable addressable evidence;
- one contestable assertion per proposed statement;
- complete assessable-content coverage accounting;
- explicit non-assertive-content treatment;
- preservation of linguistic qualifiers;
- speaker-provenance and performer-inference boundary;
- correction and potential-contradiction preservation;
- non-authoritative `ExtractionValidationObservation` semantics;
- source-attestation versus AnalystDecision boundary;
- privacy and public-repository constraints;
- explicit downstream and M2 boundaries.

## Explicit non-goals

- no schema, serialization, canonicalization, identifier, digest, or SHA algorithm;
- no executable validator, ruleset, fixture, evaluation, test, or CI;
- no prompt, agent training, fine-tuning, or runtime implementation;
- no transcription tooling, UI, draw.io, BPMN mapping, compiler, or Kernel work;
- no changes to the accepted diagnostic registry;
- no confidential or personal source content;
- no change to accepted DEC-0011 merge-strategy governance;
- no REV-0014 during conscious start.

## Deliverables

- Proposed [Structured Elicitation Extraction Contract](../../docs/STRUCTURED_ELICITATION_EXTRACTION_CONTRACT.md).
- Proposed [DEC-0010](../decisions/DEC-0010-structured-elicitation-extraction.md).
- This Proposed milestone record.
- Synchronized project memory, including PR #26 squash merge provenance.
- Issue #27 and Draft delivery PR metadata.
- Separate `OPEN-0021` governance gate tracked by Issue #28.

## Accepted dependencies

- [M1 Process IR contract](../../docs/PROCESS_IR_CONTRACT.md).
- [M1.2.1 RecordEnvelope contract](../../docs/PROCESS_IR_RECORD_ENVELOPE_CONTRACT.md).
- [M1.2.3 diagnostic policy](../../docs/PROCESS_IR_DIAGNOSTIC_POLICY_CONTRACT.md).
- [M1.2.4 staleness and revalidation contract](../../docs/ANALYST_DECISION_STALENESS_REVALIDATION_CONTRACT.md).
- [M1.2.5 mapping and target-profile contract](../../docs/MAPPING_RULE_TARGET_PROFILE_PROPAGATION_CONTRACT.md).
- DEC-0004 and DEC-0005 through DEC-0009, without amendment in this PR.

## Acceptance criteria

- [ ] A separate human semantic and design review approves the contract and DEC-0010.
- [ ] Existing source, evidence, statement, envelope, Finding, diagnostic, and AnalystDecision concepts are reused without a competing model.
- [ ] Exact evidence, derivation, atomicity, coverage, and language-preservation rules are accepted.
- [ ] Speaker provenance cannot become performer responsibility by inference.
- [ ] Corrections preserve earlier statements and potential contradiction remains non-authoritative.
- [ ] Source attestation is explicitly distinct from business-semantic acceptance.
- [ ] `ExtractionValidationObservation` has a bounded authority, lifecycle, relation to accepted records, and M2 path.
- [ ] No output or new artifact is marked Accepted before human review and authorized finalization.
- [x] Issue #28 is consciously started and resolved before REV-0014 begins or its evidence package is frozen.
- [ ] Schema, fixtures, implementation, prompts, tests, and executable validation remain deferred.

## Governance gate

Issue #28 owned merge-strategy governance independently from this milestone. Accepted DEC-0011 resolves when squash merge is permitted, when merge-commit ancestry is required, and what compensating provenance is mandatory. It extends DEC-0004 without amendment or supersession.

The M1.2.6 Draft PR does not answer or alter those questions. REV-0014 must apply DEC-0011, and this resolved gate does not grant semantic acceptance or merge authorization for M1.2.6.

## Related decisions

- [DEC-0010](../decisions/DEC-0010-structured-elicitation-extraction.md), Proposed.
- [DEC-0004](../decisions/DEC-0004-project-memory-governance.md), Accepted and unchanged.
- DEC-0005 through DEC-0009, Accepted and unchanged.

## Outcome

Proposed and in progress for semantic-design work only. No human semantic review has occurred, no acceptance transition is claimed, and no implementation has started.

## Follow-up

- Conduct a separate human semantic and design review against the exact synchronized PR #29 head.
- Apply accepted DEC-0011 to REV-0014 without changing the M1.2.6 semantic contract during this synchronization.
- Route any later machine schema and validation work to M2 and Issue #5.
- Route any later fixture or test-matrix work to separately authorized work, including Issue #21 where applicable.
