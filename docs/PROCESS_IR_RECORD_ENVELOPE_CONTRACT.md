# Process IR RecordEnvelope and Revision Semantics Contract

- Project: MøtiveFōrce
- Milestone: M1.2.1
- Status: Accepted
- Scope: RecordEnvelope and revision semantics
- Project status: Concept / pre-MVP

This is the accepted M1.2.1 design contract. Acceptance is recorded by [REV-0004](../project-memory/reviews/M1-2-1-record-envelope-semantic-design-review-3.md) and becomes repository-authoritative through merge of [PR #22](https://github.com/ThresholdOps/MotiveForce/pull/22). It is not a machine schema, not an implementation, not a persistence model, not an API design, and not an executable validator.

This contract does not amend the accepted M1 Process IR contract. It defines the accepted M1.2.1 machine-readiness representation layer for accepted M1 semantics. If a future design choice would alter accepted M1 meaning, refusal to decide remains valid until separately reviewed.

## 1. Purpose

`RecordEnvelope` is required before the project can safely define a machine schema, deterministic replay contract, decision staleness rules, persistence model, transport API, migration strategy, or executable validation.

The core rule is:

> A logical record may have many immutable revisions, but no revision may be silently mutated or silently substituted for another.

The contract defines common metadata and revision behavior for Process IR records without defining the concrete machine representation of any typed payload.

## 2. Architectural position

```text
ProcessIRPackage
  contains or references
Immutable Record Revisions
  each with
RecordEnvelope + typed record payload
  resolved through
RevisionLineage + RecordDerivationGraph + authority + context
  producing
Effective record view
```

`RecordEnvelope` is common metadata and lineage structure. Typed payloads remain defined by record-specific contracts, including the accepted M1 Process IR contract and later machine-readable schemas.

Effective views are derived from exact revisions, lineage, derivation provenance, authority, lifecycle assertions, decisions, and semantic context. The envelope is not evidence, not authority, not BPMN validation, and not a substitute for the Semantic Compiler or BPMN Kernel.

## 3. Accepted M1 basis and REV-0001 qualification

This contract is based on the accepted M1 Process IR contract in [docs/PROCESS_IR_CONTRACT.md](PROCESS_IR_CONTRACT.md), merged through [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2).

M1 acceptance provenance is qualified in [REV-0001](../project-memory/reviews/M1-process-ir-semantic-review.md):

- fully reviewed predecessor commit: [`59f1cde14c118bc8f0dcc0e1d6ebc2784a2ec600`](https://github.com/ThresholdOps/MotiveForce/commit/59f1cde14c118bc8f0dcc0e1d6ebc2784a2ec600),
- final source head: [`b2d6fe8f2192149145e04cbf2f0e5ffea737e1c0`](https://github.com/ThresholdOps/MotiveForce/commit/b2d6fe8f2192149145e04cbf2f0e5ffea737e1c0),
- squash merge commit: [`54d5e814601788574d13761561867ce5982cc88c`](https://github.com/ThresholdOps/MotiveForce/commit/54d5e814601788574d13761561867ce5982cc88c).

M1 meaning is authoritative for this design. REV-0001 defines how that semantic acceptance was reached. M1.2.1 may represent accepted meaning technically, but it MUST NOT silently reinterpret, broaden, narrow, or replace accepted M1 meaning. A conflict with M1 requires escalation rather than silent reinterpretation.

## 4. Design-choice classification register

Every material design choice in M1.2.1 is classified as one of:

- `M1-derived`: derived directly from accepted M1 semantics.
- `Technical representation`: a representation choice intended to preserve accepted M1 semantics.
- `Potential semantic change`: a choice that may alter M1 meaning and therefore requires escalation.

| Choice ID | Design choice | Classification | M1 basis | Rationale | Escalation required | Related Issue or decision |
| --- | --- | --- | --- | --- | --- | --- |
| `REC-CHOICE-001` | Separate logical `record_id` from immutable `revision_id`. | Technical representation | M1 requires stable identifiers and provenance preservation. | A logical assertion can be corrected without rewriting history. | No, unless the split is later used to weaken exact provenance. | [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16), [DEC-0005](../project-memory/decisions/DEC-0005-record-envelope-revision-semantics.md) |
| `REC-CHOICE-002` | Treat released revisions as immutable. | M1-derived | M1 requires immutable evidence fragments and traceable rejected or superseded interpretations. | Immutability protects auditability across review and compilation. | No. | [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16) |
| `REC-CHOICE-003` | Require exact revision references for authoritative use. | Technical representation | M1 requires traceable references across review and compilation. | Exact references prevent silent retargeting after supersession. | No, unless future usability rules weaken authority boundaries. | [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16) |
| `REC-CHOICE-004` | Derive effective status rather than storing it as self-authorizing truth. | M1-derived | M1 distinguishes proposal, acceptance, compilation, and validation authority. | Status must come from valid authority and context, not from a writable field alone. | No. | [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16) |
| `REC-CHOICE-005` | Do not automatically inherit acceptance onto a new revision. | Potential semantic change | M1 requires explicit authority for acceptance but did not define cross-revision carry-forward behavior. | The conservative rule prevents authority leakage and is accepted by REV-0004 as the M1.2.1 default. It does not retroactively change M1 records. | Resolved and accepted by REV-0004. Controlled carry-forward remains deferred to Issue #19. | [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16), [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19), [REV-0002](../project-memory/reviews/M1-2-1-record-envelope-semantic-design-review.md), [REV-0003](../project-memory/reviews/M1-2-1-record-envelope-semantic-design-review-2.md), [REV-0004](../project-memory/reviews/M1-2-1-record-envelope-semantic-design-review-3.md) |
| `REC-CHOICE-006` | Keep revision graph conflicts explicit. | M1-derived | M1 requires unresolved ambiguity and contradiction to remain explicit. | Multiple heads cannot be silently ordered by confidence or creation time. | No. | [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16) |
| `REC-CHOICE-007` | Use digest descriptors conceptually without selecting an algorithm. | Technical representation | M1 defers machine schema and implementation details. | Integrity metadata is useful, but hash and canonicalization choices belong later. | No. | [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16), [Issue #5](https://github.com/ThresholdOps/MotiveForce/issues/5) |
| `REC-CHOICE-008` | Classify revision impact. | Technical representation | M1 distinguishes business meaning, provenance, modeling policy, and authority. | Impact classification supports later staleness and replay rules. | Yes when impact is material to authority carry-forward. | [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16), [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19) |
| `REC-CHOICE-009` | Bind M1 value-state dimensions and their semantic bases to exact subject revisions; preservation requires explicit reviewed confirmation. | Potential semantic change | M1 defines the four-axis model but not cross-revision behavior. | The rule preserves M1 traceability and is accepted by REV-0004 with the reviewed preservation-assertion model. | Resolved and accepted by REV-0004. Later aggregation policies require separate acceptance. | [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16), [REV-0002](../project-memory/reviews/M1-2-1-record-envelope-semantic-design-review.md), [REV-0003](../project-memory/reviews/M1-2-1-record-envelope-semantic-design-review-2.md), [REV-0004](../project-memory/reviews/M1-2-1-record-envelope-semantic-design-review-3.md) |
| `REC-CHOICE-010` | Separate same-record `RevisionLineage` from cross-record `RecordDerivationGraph`. | Technical representation | M1 requires stable traceability but does not require derivation to change source status. | Same-record revision heads and cross-record provenance have different semantics. | Required only if later rules use derivation to transfer authority or change source-record status. | [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16) |
| `REC-CHOICE-011` | Represent effective-status bases as separate revisioned records rather than revisions of the subject payload. | M1-derived | M1 separates proposal, human decision, acceptance, compilation eligibility, and validation authorities and artifacts. | A status outcome is derived from separate authority bases and must not mutate the subject payload. | No. | [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16) |
| `REC-CHOICE-012` | Use released/addressable revision as the immutability boundary; edit buffers are outside the contract. | Technical representation | M1 requires immutable addressable evidence and traceable records but does not define edit-buffer mechanics. | Immutability needs a clear boundary without constraining UI drafting behavior. | No, unless later tooling exposes editable addressable revisions. | [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16) |
| `REC-CHOICE-013` | Generalize exact basis references to external authoritative bases outside Process IR. | Technical representation | M1 requires traceability without requiring every source artifact to become a Process IR record. | External bases can be exact through immutable locator, version identifier, content identifier, or versioned locator plus integrity descriptor. | No, unless external exactness is later used to bypass Process IR authority. Accepted by REV-0004. | [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16), [REV-0003](../project-memory/reviews/M1-2-1-record-envelope-semantic-design-review-2.md), [REV-0004](../project-memory/reviews/M1-2-1-record-envelope-semantic-design-review-3.md) |
| `REC-CHOICE-014` | Limit current effective-status derivation until Issue #19 defines accepted staleness and invalidation policy. | Technical representation | M1 accepts exact authority and context boundaries but defers machine-level staleness mechanics. | Historical/as-of replay remains possible, but current status needs staleness policy. | No for the boundary; detailed policy remains deferred to [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19). Accepted by REV-0004. | [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16), [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19), [REV-0003](../project-memory/reviews/M1-2-1-record-envelope-semantic-design-review-2.md), [REV-0004](../project-memory/reviews/M1-2-1-record-envelope-semantic-design-review-3.md) |

The historical `Potential semantic change` classification records why escalation was required. For `REC-CHOICE-005` and `REC-CHOICE-009`, that escalation is resolved and accepted by REV-0004 for M1.2.1.

Current human-review disposition:

- `REC-CHOICE-005` is accepted as the conservative default: no automatic authority or acceptance carry-forward between revisions. Detailed controlled carry-forward remains deferred to [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19).
- `REC-CHOICE-009` is accepted with the reviewed preservation-assertion model.
- Generalized exact-reference requirements for external authoritative bases are accepted.
- The boundary between historical/as-of effective-status derivation and authoritative current-status derivation is accepted. Authoritative current status remains bounded by `EFFECTIVE_STATUS_STALENESS_UNDETERMINED` until Issue #19 defines an Accepted policy.

## 5. Scope and explicit non-goals

### In scope

- common envelope concepts,
- logical identity,
- revision identity,
- immutable released revisions,
- `RevisionLineage`,
- `RecordDerivationGraph`,
- supersession,
- branching and merge conflict behavior,
- revision-scoped M1 value-state assessments,
- effective-status derivation inputs,
- subject and status-basis separation,
- reference resolution,
- authorship versus authority,
- provenance references,
- digest descriptor concept,
- conservative authority carry-forward default,
- diagnostics,
- synthetic examples.

### Explicit non-goals

- JSON Schema or any machine schema,
- concrete programming-language classes,
- database tables,
- storage implementation,
- API design,
- timestamp wire format,
- identifier syntax,
- hash algorithm selection,
- canonical JSON or XML selection,
- migration implementation,
- deterministic compiler replay implementation,
- detailed `AnalystDecision` staleness policy,
- complete extension mechanism,
- UI edit-buffer workflow,
- code or tests.

## 6. Normative terminology

- `logical record`: one conceptual Process IR record across revisions, identified by `record_id`.
- `record revision`: one immutable version of a logical record, identified by `revision_id` after release.
- `released revision`: a record revision that has been assigned a stable `revision_id` and has been included in an addressable `ProcessIRPackage` or published as an independently addressable record.
- `edit buffer`: pre-release draft content outside the `RecordEnvelope` contract.
- `RecordEnvelope`: common metadata, identity, context, provenance, integrity, and lineage structure attached to a typed payload.
- `typed payload`: the record-specific content governed by the relevant semantic contract.
- `RevisionLineage`: a same-record directed acyclic graph connecting revisions that belong to exactly one `record_id`.
- `RecordDerivationGraph`: a cross-record graph connecting exact revisions of different logical records for derivation, split, transformation, or semantic merge provenance.
- `initial revision`: the first released revision of a logical record.
- `predecessor revision`: a prior same-record revision referenced by a successor revision in `RevisionLineage`.
- `successor revision`: a same-record revision that references one or more predecessor revisions in `RevisionLineage`.
- `status-basis record`: a separate revisioned record such as an `AnalystDecision`, lifecycle assertion, authority reference, or policy basis used to derive status for a subject revision.
- `subject revision`: the exact revision whose payload is being evaluated, decided, compiled, or validated.
- `reviewed preservation assertion`: a separate exact revisioned semantic basis record, or equivalent exact revisioned semantic record, that authoritatively confirms a four-axis value-state assessment remains unchanged across a successor revision.
- `external authoritative basis`: an evidence, authority, context, rule, condition, policy, mapping, profile, source, or other basis outside the Process IR identity domain that affects authoritative output.
- `supersession`: a same-record lineage relation indicating that a later revision replaces a prior revision for a stated context or purpose.
- `revision head`: a same-record revision that currently has no successor in a given lineage branch.
- `effective revision`: the same-record revision selected by an explicit resolution policy, authority basis, and context for a stated use.
- `effective status`: a derived lifecycle status for a subject revision in a context.
- `exact revision reference`: a reference to a specific `revision_id` or equivalent immutable locator for external artifacts outside Process IR revision scope.
- `logical-record reference`: a reference to `record_id` without selecting a specific revision.
- `floating reference`: any reference that requires a resolution policy to select a revision at use time.
- `revision impact`: classification of what changed between revisions.
- `integrity descriptor`: metadata describing digest scope, algorithm reference, canonicalization profile reference, and digest value.
- `provenance reference`: a link to evidence, decision, source artifact, prior revision, policy, or repository artifact supporting the record.

The word "latest" MUST NOT be used as an authoritative concept unless an explicit resolution policy defines how "latest" is determined and whether it is permitted for the requested use.

## 7. RecordEnvelope minimum conceptual content

| Field or concept | Requirement | Purpose | Authority implications | Notes or deferred implementation choice |
| --- | --- | --- | --- | --- |
| `envelope_version` | MUST exist. | Identifies the envelope convention. | Does not establish record authority. | Exact versioning syntax is deferred. |
| `record_id` | MUST exist. | Identifies the logical record. | Not interchangeable with `revision_id`. | Global uniqueness mechanism is deferred. |
| `revision_id` | MUST exist for released revisions. | Identifies one immutable released revision. | Authoritative references normally target this identifier. | Syntax is deferred. |
| `record_kind` | MUST exist. | Names the typed payload family. | Does not validate the payload by itself. | Must align with later payload contracts. |
| `record_contract_version_ref` | SHOULD exist when the payload contract is versioned. | Identifies the payload contract basis. | Does not make an unsupported payload valid. | Detailed compatibility rules are deferred. |
| package or identity-scope reference | SHOULD exist where identifiers are scoped. | Prevents accidental identifier collisions. | Does not authorize cross-package use. | Scope mechanics are deferred. |
| predecessor revision references | REQUIRED except for initial revisions, but only within same-record `RevisionLineage`. | Preserves same-record lineage. | Unresolved predecessors block authoritative use. | Multiple predecessors are allowed only for merge revisions of the same logical record. |
| derivation references | MAY exist for cross-record provenance. | Preserves split, transformation, and semantic merge provenance. | Does not supersede source records or transfer authority. | Modeled through `RecordDerivationGraph`. |
| lineage relation kind | SHOULD exist for successor revisions. | Distinguishes same-record supersession, branch, and merge. | Cannot silently supersede unrelated records. | Exact enum is deferred. |
| initial-revision indication | REQUIRED for initial revisions. | Avoids ambiguous missing predecessor data. | Does not imply acceptance. | Could be derived in a future schema. |
| revision-impact classification | SHOULD exist for successor revisions. | Supports review and later staleness policies. | Does not carry authority. | `impact undetermined` blocks assessment preservation and authority carry-forward. |
| rationale for revision | SHOULD exist for successor revisions. | Explains why a new revision exists. | Rationale is not evidence unless backed by evidence references. | Free-text format is deferred. |
| creator or author actor reference | SHOULD exist. | Records authorship or origin. | Authorship is not authority. | Identity representation remains open. |
| record creation time concept | SHOULD exist. | Supports ordering and audit. | Creation time cannot resolve semantic ambiguity alone. | Timestamp wire format is deferred. |
| semantic effective time | MUST be represented through exact `SemanticContext` basis where relevant. | Separates business time from technical creation time. | Context controls semantic applicability. | Inherits M1 `SemanticContext` rules. |
| `context_ref` | MUST resolve to the exact applicable context revision where context is revisioned and M1 requires context. | Scopes meaning. | Missing or floating context can block authoritative use. | Package defaults must be explicit and exact where revisioned. |
| provenance references | MUST exist where content is source-derived or decision-derived. | Preserves traceability. | Provenance is support, not authority by itself. | Reference syntax is deferred. |
| evidence references | MUST resolve exactly where evidence is revisioned and M1 requires evidence. | Supports accepted source-derived assertions. | Evidence cannot be replaced by the envelope. | External immutable evidence may use exact locators or digests. |
| decision or authority references | MUST resolve exactly where status or acceptance depends on revisioned authority. | Connects status to authorized decisions. | Must reference valid authority basis. | `DecisionAuthorityRef` semantics remain M1. |
| external authoritative basis references | MUST be exact when external bases affect authoritative output. | Allows non-Process IR bases without inventing Process IR revision IDs. | Exactness is necessary but not authority by itself. | Uses immutable external locator, explicit external version identifier, immutable content identifier, or versioned locator plus integrity descriptor where applicable. |
| source package reference | SHOULD exist when revisions move between packages. | Preserves source package provenance. | Does not authorize import. | Import policy is deferred. |
| content digest descriptor | MAY exist. | Supports integrity checking. | Digest is not evidence or authority. | Algorithm and canonicalization are deferred. |
| algorithm reference | REQUIRED when digest value exists. | Explains how digest was produced. | Algorithm choice does not prove business truth. | Concrete algorithm deferred. |
| canonicalization profile reference | REQUIRED when digest value depends on canonical form. | Makes digest reproducible. | Does not authorize mutation. | Concrete profile deferred. |
| digest value | MAY exist. | Records integrity output. | Matching digest does not validate semantics. | Format deferred. |
| digest scope | REQUIRED when digest value exists. | Defines what was hashed. | Prevents false equivalence between payload-only and envelope-plus-payload digests. | Scope taxonomy deferred. |

Directly authored envelope content MUST NOT treat the following as self-authorizing facts:

- effective status,
- authority,
- BPMN validity,
- current effective revision,
- successful compilation.

A cached derived value MAY exist later only if clearly marked as derived and accompanied by derivation basis and policy version.

## 8. Identity model

`record_id` identifies one logical record across revisions. `revision_id` identifies exactly one immutable released revision. They are not interchangeable.

Exact identifier syntax and global-uniqueness mechanisms remain deferred. Identifiers MUST be stable within their declared identity scope.

A correction to the same logical meaning normally retains `record_id` and creates a new `revision_id`. A genuinely new logical record receives a new `record_id`.

A split creates new logical records when one prior record is separated into independently disputable meanings. The derived records MUST reference the prior exact revision through `RecordDerivationGraph`. A semantic merge of different logical records creates a new logical record with a new `record_id`, linked to source exact revisions through `RecordDerivationGraph`.

An identifier MUST NOT be silently reused for semantically different content.

## 9. Released revision boundary and immutability rules

A released revision is a record revision that has been assigned a stable `revision_id` and has been included in an addressable `ProcessIRPackage` or published as an independently addressable record.

Rules:

- a released revision is immutable,
- an edit buffer before release is outside the `RecordEnvelope` contract,
- publishing or packaging the revision establishes the immutable boundary,
- assigning a provisional UI identifier alone does not necessarily release a revision,
- exact implementation mechanics remain deferred,
- a system MUST NOT expose an addressable revision and later treat it as an editable draft.

Correction creates a new revision. A status change does not mutate an existing subject revision. Source evidence remains immutable as required by M1.

Historical revisions remain addressable. Physical deletion MUST NOT be used to erase semantic history. Rejected, deferred, and superseded material remains traceable. A digest or metadata mismatch does not authorize rewriting the old revision.

Diagnostics:

- `IMMUTABILITY_VIOLATION`: general diagnostic emitted when immutable revision semantics are violated.
- `RELEASED_REVISION_MUTATION`: primary immutability case emitted when a released revision is altered, erased, or retargeted instead of creating a new revision.

## 10. RevisionLineage and RecordDerivationGraph

### RevisionLineage

`RevisionLineage` contains revisions belonging to exactly one `record_id`. It is a directed acyclic graph. It supports ordinary revision supersession, branching, and merge of branch revisions of the same logical record.

`RevisionLineage` determines candidate revision heads for one logical record and may affect effective-revision resolution for that logical record.

A `RevisionLineage` edge MUST NOT connect different `record_id` values.

### RecordDerivationGraph

`RecordDerivationGraph` connects exact revisions belonging to different logical records. It preserves provenance for:

- `derived-from`,
- `split-from`,
- semantic merge from multiple logical records,
- transformation into a new logical record.

`RecordDerivationGraph` does not make a source record superseded, does not change the source record's effective revision or effective status, and does not transfer authority, acceptance, value-state assessment, or context automatically.

### Merge distinctions

A merge of concurrent revisions of the same `record_id` creates one successor revision in `RevisionLineage`.

A semantic merge of different logical records creates a new logical record with a new `record_id`, linked through `RecordDerivationGraph`.

A cross-record merge MUST NOT masquerade as a same-record revision.

Diagnostics:

- `REVISION_REFERENCE_UNRESOLVED`,
- `REVISION_CYCLE`,
- `MULTIPLE_EFFECTIVE_REVISIONS`,
- `INVALID_REVISION_LINEAGE`,
- `CROSS_RECORD_REVISION_LINEAGE`,
- `RECORD_DERIVATION_REFERENCE_UNRESOLVED`,
- `INVALID_RECORD_DERIVATION`.

`MULTIPLE_EFFECTIVE_REVISIONS` applies to unresolved candidate heads for the same logical record and context, not to unrelated derived records.

## 11. Revision impact classification

Conceptual revision-impact classes:

- semantic-content change,
- provenance correction,
- administrative metadata change,
- status or authority-basis change,
- impact undetermined.

Revision impact is not authority. An Analytical Agent MAY propose impact classification. Material classification requires review when it affects value-state preservation, acceptance carry-forward, or staleness behavior. `impact undetermined` blocks assessment preservation, authority carry-forward, and authoritative compilation of the affected value.

This contract does not complete the detailed `AnalystDecision` staleness policy; that remains tracked by [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19).

Diagnostic:

- `REVISION_IMPACT_UNDETERMINED`.

## 12. Revision-scoped M1 value-state semantics

M1 defines the four-axis value-state model:

- `knowledge_state`,
- `applicability`,
- `requirement_state`,
- `value_presence`.

Core rule:

> A four-axis value-state assessment is bound to an exact record revision, its exact semantic basis revisions, and the applicable `SemanticContext`. No axis is inherited, preserved, or recomposed across revisions by omission or by selecting a later revision.

Each four-axis assessment MUST identify:

- subject `revision_id`,
- `context_ref` resolving to the exact applicable context revision where revisioned,
- evidence and rule basis revisions,
- condition basis revisions where conditionality applies,
- assessment or decision basis revision where applicable.

A successor revision MUST explicitly either provide a new four-axis assessment or reference an explicit reviewed preservation assertion that all four dimensions and their bases remain semantically unchanged.

A reviewed preservation assertion MUST NOT become self-authorizing metadata. It MUST be an explicit, separately identifiable revisioned basis record or equivalent exact revisioned semantic record. It is not a Boolean flag or mutable field on the successor revision.

A reviewed preservation assertion MUST reference:

- the exact predecessor assessment revision,
- the exact successor subject revision,
- the exact predecessor and successor semantic basis sets,
- the exact applicable `SemanticContext`,
- the reviewed revision-impact classification,
- the comparison rationale and outcome.

It MUST explicitly confirm that all four dimensions remain semantically unchanged:

- `knowledge_state`,
- `applicability`,
- `requirement_state`,
- `value_presence`.

It MUST explicitly confirm that no evidence, rule, condition, context, authority, policy, or semantic payload change invalidates preservation.

The Analytical Agent MAY propose a preservation assertion but cannot authorize it. When preservation affects accepted business meaning or authority, it requires a valid exact `DecisionAuthorityRef`, unless a later Accepted deterministic policy explicitly authorizes controlled automated confirmation.

Omission, matching labels, matching digests, matching payload text, or unchanged `record_id` MUST NOT constitute preservation.

Omission MUST NOT mean inheritance.

Reevaluation is REQUIRED when any of these changes:

- semantic value,
- evidence,
- source interpretation,
- `SemanticContext`,
- process version or variant,
- applicability rule,
- requirement rule,
- condition or condition result,
- authority basis,
- revision-impact classification is `impact undetermined`.

A provenance-only or administrative revision MAY preserve the prior assessment only when:

- the revision impact is explicitly reviewed as non-semantic,
- the exact prior assessment and basis revisions are referenced,
- context remains compatible,
- no evidence, rule, condition, authority, or semantic payload changed.

An effective view MUST NOT compose `knowledge_state` from one subject revision, `applicability` from another, `requirement_state` from another, or `value_presence` from another unless a later accepted aggregation contract explicitly permits it.

Ambiguity or contradiction in a predecessor does not disappear merely because a successor revision exists.

Known absence, unknown, ambiguity, contradiction, applicability, requirement, and presence retain their accepted M1 meanings.

`revision-impact = impact undetermined` blocks assessment preservation, authority carry-forward, and authoritative compilation of the affected value.

Diagnostics:

- `VALUE_STATE_REEVALUATION_REQUIRED`,
- `VALUE_STATE_BASIS_STALE`,
- `CROSS_REVISION_VALUE_STATE_COMPOSITION`,
- `VALUE_STATE_PRESERVATION_BASIS_INVALID`.

## 13. Reference semantics

Default rule:

> Authoritative references MUST resolve to an exact `revision_id`.

For authoritative derivation and compilation, exact revision references are required for every revisioned basis, including:

- subject record revision,
- `AnalystDecision` revision,
- `DecisionAuthorityRef` revision,
- `SemanticContext` revision,
- lifecycle or status assertion revision,
- evidence revision,
- `SourceArtifact` or source-record revision where revisioned,
- applicable business-rule revision,
- condition and condition-result revisions,
- modeling or compilation-policy revision affecting the outcome,
- mapping-rule revision where used,
- target BPMN profile revision where revisioned.

Exact subject reference plus floating authority, context, evidence, rule, condition, or policy basis is not sufficient. Supersession does not silently retarget any basis. An effective view MUST expose the complete exact basis set.

Every authoritative basis represented as a revisioned Process IR record MUST resolve to an exact `revision_id`.

Every authoritative external basis outside Process IR MUST resolve through one of:

- an immutable external locator,
- an explicit external version identifier,
- an immutable content identifier,
- a versioned locator plus integrity descriptor where applicable.

This applies to external evidence, authority sources, semantic contexts, business rules, conditions, policies, mappings, target BPMN profiles, source artifacts, and other bases affecting authoritative output.

`current`, `latest`, an unversioned mutable URL, or silent repository-head resolution is not exact. The effective basis set MUST expose how each external reference was made exact.

Digests remain integrity descriptors, not evidence and not authority. No artificial Process IR `revision_id` needs to be invented for an external artifact outside the Process IR identity domain.

References only to `record_id` are logical or floating references. Floating references MUST declare a resolution policy. Silent "resolve to latest" behavior is forbidden.

Accepted `AnalystDecision` records MUST identify the exact revisions they decide. Compilation MUST record the exact input revisions used. A stale or unresolved basis produces a diagnostic.

Diagnostics:

- `FLOATING_REFERENCE_NOT_ALLOWED`,
- `FLOATING_AUTHORITY_BASIS`,
- `FLOATING_CONTEXT_BASIS`,
- `FLOATING_EVIDENCE_BASIS`,
- `FLOATING_EXTERNAL_BASIS`,
- `STALE_REVISION_REFERENCE`,
- `STATUS_BASIS_REFERENCE_UNRESOLVED`,
- `REVISION_REFERENCE_UNRESOLVED`.

## 14. Subject record and status-basis separation

Core rule:

> A change in the derived effective status of a subject revision does not mutate that revision and does not, by itself, create a successor revision of the subject record. The status basis is represented by separate exact revisioned records.

A subject record revision contains the subject payload, remains immutable, and does not store self-authorizing effective status.

Status-basis records may include:

- `AnalystDecision`,
- lifecycle assertion,
- rejection or deferral record,
- supersession assertion where modeled separately,
- authority reference,
- policy basis.

Every status-basis record has its own `record_id`, its own `revision_id`, its own lineage, and exact references to the subject revision and other bases.

Example rule:

- activity revision `R1` remains `R1`,
- decision revision `D1` accepts exact `R1`,
- effective view derives accepted for `R1`,
- replacing the decision creates `D2`,
- it does not create `R2` of the activity unless the activity payload itself changes.

Changing an effective-status outcome means adding, revising, rejecting, superseding, or invalidating a status-basis record and recomputing the effective view. It never means rewriting the subject revision.

Remediation text such as "return to proposed status" means remove or invalidate the unauthorized status basis and derive the resulting status again. It does not mean mutate a stored status field on the subject.

Diagnostics:

- `STATUS_BASIS_REFERENCE_UNRESOLVED`,
- `SUBJECT_REVISION_STATUS_MUTATION`.

## 15. Authorship versus authority

`created_by_actor_ref` proves authorship or origin, not decision authority.

An Analytical Agent MAY create proposed revisions. An agent cannot create authoritative acceptance. `DecisionAuthorityRef` remains the basis for authoritative human decisions. A `RecommendedDecision` is not authority. Envelope metadata cannot elevate a proposal to accepted. Successful storage, digest verification, or compilation cannot establish authority.

Diagnostic:

- `UNAUTHORIZED_STATUS_BASIS`.

## 16. Effective-status derivation

`effective_status` is derived, not freely authored.

Derivation must consider at least:

- exact subject record revision,
- exact lifecycle or status-basis records,
- valid `AnalystDecision` revision where applicable,
- valid `DecisionAuthorityRef` revision where revisioned,
- exact `SemanticContext` revision where revisioned,
- effective time,
- `RevisionLineage`,
- supersession,
- rejection or deferral,
- conflicting decisions,
- dependency validity,
- exact evidence, rule, condition, and policy basis revisions where they affect the outcome.

Deterministic conceptual outcomes:

- proposed,
- under-review,
- accepted,
- rejected,
- deferred,
- superseded,
- unresolved or conflict where no single effective status can be established.

This does not add a new authoritative M1 lifecycle state silently. "Unresolved" or "conflict" may be a derivation outcome or diagnostic condition, not a replacement for accepted M1 vocabulary.

No directly stored field may override invalid authority or unresolved lineage.

Until an Accepted `AnalystDecision` staleness and invalidation policy exists, authoritative effective-status derivation is limited to an exact closed basis set evaluated within an explicit `SemanticContext` and as-of effective time.

Successful resolution of every referenced revision does not establish that the basis set remains current.

When a request for authoritative current effective status requires a staleness judgment not defined by an Accepted policy, the system MUST NOT infer a current status. It MUST produce an unresolved result and `EFFECTIVE_STATUS_STALENESS_UNDETERMINED`.

Historical replay or as-of derivation against the exact closed basis set remains permitted.

`EFFECTIVE_STATUS_STALENESS_UNDETERMINED` does not mean that the historical decision never existed. It means continued current authority cannot be established under available Accepted policies. Exact references resolving successfully are necessary but not sufficient for current validity. The BPMN Kernel MUST NOT resolve this condition. The Semantic Compiler MUST NOT bypass it through partial compilation.

[Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19) remains responsible for detailed staleness, invalidation, revalidation, and controlled authority carry-forward policy. Issue #19 remains open and deferred.

Diagnostics:

- `EFFECTIVE_STATUS_UNRESOLVED`,
- `CONFLICTING_STATUS_BASIS`,
- `UNAUTHORIZED_STATUS_BASIS`,
- `STATUS_BASIS_REFERENCE_UNRESOLVED`,
- `EFFECTIVE_STATUS_STALENESS_UNDETERMINED`.

## 17. Authority carry-forward across revisions

The accepted conservative rule is:

> Acceptance and other authoritative decisions attach to the exact revision or revisions they reference. A new revision does not inherit authority automatically.

Therefore:

- semantic correction requires new review or decision,
- provenance-only or administrative changes do not automatically inherit acceptance,
- a later accepted policy MAY define a controlled confirmation or carry-forward mechanism,
- no implicit carry-forward is permitted by this accepted M1.2.1 contract,
- [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19) remains responsible for detailed staleness and controlled confirmation or carry-forward policy.

This conservative rule is accepted by REV-0004 as a safety rule. It does not retroactively change M1 records. The historical `Potential semantic change` classification records why escalation was required; the escalation is resolved for M1.2.1 by REV-0004. Any future controlled carry-forward mechanism requires a later Accepted policy.

## 18. Provenance and integrity descriptors

Provenance references explain where content and decisions came from. Digest descriptors support integrity checking.

A digest is not evidence. A digest is not authority. A matching digest does not prove business truth. A digest mismatch does not permit mutation of the original revision.

When a digest is used, the algorithm reference and canonicalization profile reference MUST be explicit. Concrete algorithm and canonicalization selections remain deferred.

Diagnostics:

- `INTEGRITY_DESCRIPTOR_INCOMPLETE`,
- `INTEGRITY_MISMATCH`.

These diagnostics may become executable only in M2 or later.

## 19. Package and compiler interaction

`ProcessIRPackage` MAY include or reference exact record revisions. Package assembly MUST NOT silently choose among multiple heads. A package MUST preserve revision, derivation, status-basis, value-state, and exact-basis provenance.

Semantic Compiler input MUST resolve to exact revisions for every revisioned subject, authority, context, evidence, rule, condition, mapping, target profile, and policy basis. `CompiledSemanticModel` elements MUST retain exact revision provenance. Partial compilation MUST NOT bypass unresolved revision lineage, unresolved derivation, stale value-state basis, or floating authoritative basis. The BPMN Kernel remains downstream and does not resolve revision authority.

## 20. Required diagnostics catalogue

| Diagnostic | Meaning | Typical blocking behavior | Affected scope | Expected remediation | Authority implications |
| --- | --- | --- | --- | --- | --- |
| `IMMUTABILITY_VIOLATION` | Immutable revision semantics were violated. | Blocking. | Affected revision and dependent references. | Restore immutable revision provenance and create a successor revision for corrections. | Mutation cannot create authority. |
| `RELEASED_REVISION_MUTATION` | A released revision was altered, erased, or retargeted. | Blocking. | Affected released revision and dependents. | Restore the released revision and express changes as a new revision. | Addressable records cannot become editable drafts. |
| `REVISION_REFERENCE_UNRESOLVED` | A referenced `revision_id` cannot be resolved. | Blocking for authoritative use. | Referencing record, package, decision, or compilation request. | Provide the missing revision, correct the reference, or exclude the affected scope. | Unresolved references cannot support decisions or compilation. |
| `REVISION_CYCLE` | Same-record `RevisionLineage` contains a cycle. | Blocking. | Affected lineage component. | Correct lineage references. | Cyclic lineage cannot establish effective status. |
| `INVALID_REVISION_LINEAGE` | Same-record lineage relation is incompatible with record identity or declared relation. | Blocking where lineage affects status or provenance. | Affected logical record. | Correct relation kind or defer. | Invalid lineage cannot carry authority. |
| `CROSS_RECORD_REVISION_LINEAGE` | A same-record lineage edge connects different `record_id` values. | Blocking. | Affected records and lineage. | Replace with `RecordDerivationGraph` or create valid same-record revisions. | Cross-record derivation cannot supersede source records. |
| `RECORD_DERIVATION_REFERENCE_UNRESOLVED` | A derivation edge references an unavailable exact source or target revision. | Blocking where derivation provenance is required. | Affected derived record. | Provide or correct the exact derivation reference. | Unresolved derivation cannot transfer evidence or meaning. |
| `INVALID_RECORD_DERIVATION` | Derivation is structurally or semantically incompatible with the declared relation. | Blocking where derivation affects use. | Affected derived record and source references. | Correct derivation relation, split records, or defer. | Derivation cannot create authority. |
| `MULTIPLE_EFFECTIVE_REVISIONS` | More than one candidate effective revision exists for the same logical record and context without a resolution basis. | Blocking for authoritative use. | Affected logical record in context. | Merge, decide, defer, or define an explicit resolution policy where allowed. | The system cannot silently choose a head. |
| `VALUE_STATE_REEVALUATION_REQUIRED` | A successor revision lacks a valid new four-axis assessment or explicit preservation basis after a relevant change. | Blocking for authoritative use of the affected value. | Affected value assessment and subject revision. | Create a new assessment or reviewed preservation assertion. | Value-state authority cannot be inherited by omission. |
| `VALUE_STATE_BASIS_STALE` | An assessment references evidence, context, rules, conditions, decisions, or authority revisions that are superseded or incompatible for the requested context. | Blocking for authoritative use of the affected value. | Affected assessment and basis set. | Reevaluate against current exact bases or intentionally use a historical context. | Stale basis cannot support current authority. |
| `CROSS_REVISION_VALUE_STATE_COMPOSITION` | An effective view constructs one four-axis assessment from dimensions belonging to different subject revisions without an accepted aggregation policy. | Blocking. | Affected effective view. | Use one exact assessment or define a later accepted aggregation contract. | Mixed axes cannot create authoritative value state. |
| `VALUE_STATE_PRESERVATION_BASIS_INVALID` | A preservation assertion is missing, incomplete, unauthorized, mutable, floating, or represented as self-authorizing metadata. | Blocking for reuse of the prior assessment. | Successor subject revision and value-state basis set. | Provide a valid exact revisioned preservation assertion with authority where required, or reevaluate. | Preservation cannot be authorized by labels, digests, payload equality, or agent proposal alone. |
| `FLOATING_REFERENCE_NOT_ALLOWED` | A reference uses `record_id` without an allowed resolution policy. | Blocking for authoritative use. | Decision, package, or compiler request using the reference. | Replace with exact `revision_id` or define an approved policy where floating use is non-authoritative. | Floating reference cannot establish accepted scope. |
| `FLOATING_AUTHORITY_BASIS` | Authority basis references a revisioned decision, authority, lifecycle assertion, or policy without an exact revision. | Blocking where authority affects use. | Affected effective status, decision, or compilation scope. | Resolve every authority basis to exact revisions. | Floating authority is not reproducible. |
| `FLOATING_CONTEXT_BASIS` | Context basis floats to current or latest rather than an exact `SemanticContext` revision where context is revisioned. | Blocking where context affects meaning. | Affected assertion, assessment, decision, or compilation scope. | Resolve context to an exact revision or immutable external locator. | Meaning cannot be scoped reproducibly. |
| `FLOATING_EVIDENCE_BASIS` | Evidence basis floats rather than resolving to an exact evidence revision or immutable external locator. | Blocking where evidence supports accepted source-derived meaning. | Affected assertion or assessment. | Resolve evidence exactly or provide immutable external locator and digest where applicable. | Evidence support cannot be silently retargeted. |
| `FLOATING_EXTERNAL_BASIS` | An external authoritative basis uses current, latest, an unversioned mutable URL, silent repository-head resolution, or another non-exact reference. | Blocking where the external basis affects authoritative output. | Affected basis set and dependent output. | Provide immutable locator, explicit version identifier, immutable content identifier, or versioned locator plus integrity descriptor where applicable. | External exactness is required without inventing Process IR revision IDs. |
| `STALE_REVISION_REFERENCE` | A reference targets a superseded or invalidated revision where current context requires review. | Blocking when stale use affects authority. | Referencing record or compilation scope. | Revalidate, issue a new decision, or intentionally use the historical revision with context. | Stale references cannot silently inherit authority. |
| `STATUS_BASIS_REFERENCE_UNRESOLVED` | A status-basis record or one of its exact references cannot be resolved. | Blocking for effective-status derivation. | Subject revision and status-basis set. | Provide or correct the missing status-basis revision. | Effective status cannot be derived from missing bases. |
| `SUBJECT_REVISION_STATUS_MUTATION` | A system mutates or creates a subject revision solely to encode a derived status change without subject-payload change. | Blocking. | Subject record and status-basis records. | Represent the change as a separate status-basis revision and recompute effective view. | Status authority does not mutate payload. |
| `REVISION_IMPACT_UNDETERMINED` | Revision impact cannot be classified. | Blocking for value-state preservation, authority carry-forward, and staleness decisions. | Affected successor revision. | Review impact classification or defer affected authority use. | No assessment or authority carry-forward is allowed. |
| `EFFECTIVE_STATUS_UNRESOLVED` | No single effective status can be derived. | Blocking for authoritative use. | Affected revision and dependent records. | Resolve status basis, authority, lineage, context, or exact basis set. | Authored status labels are insufficient. |
| `EFFECTIVE_STATUS_STALENESS_UNDETERMINED` | A request for current authoritative status depends on staleness or invalidation judgment not defined by an Accepted policy. | Blocking for current authoritative result; non-blocking for exact historical/as-of replay. | Subject revision and closed basis set. | Return unresolved for current status, perform as-of derivation if requested, or wait for Issue #19 policy. | Continued current authority cannot be inferred from exact reference resolution alone. |
| `CONFLICTING_STATUS_BASIS` | Valid-looking status bases conflict. | Blocking. | Affected revision, context, and decisions. | Obtain authorized resolution or split scope. | Conflicting authority bases cannot both control. |
| `UNAUTHORIZED_STATUS_BASIS` | A status relies on authorship, metadata, or invalid authority. | Blocking. | Affected status or lifecycle assertion. | Provide valid exact `DecisionAuthorityRef` basis or remove or invalidate the unauthorized basis and recompute. | Authorship and storage do not create authority. |
| `INTEGRITY_DESCRIPTOR_INCOMPLETE` | Digest metadata lacks required algorithm, canonicalization, value, or scope. | Blocking only where digest validation is required. | Affected integrity descriptor. | Complete descriptor or mark integrity validation unavailable. | Digest absence does not remove evidence, but cannot support integrity claims. |
| `INTEGRITY_MISMATCH` | Computed integrity does not match descriptor. | Blocking where integrity is required. | Affected revision or package. | Investigate provenance and create corrective revision if needed. | Mismatch does not authorize rewriting history. |
| `SEMANTIC_CHANGE_ESCALATION_REQUIRED` | A representation choice appears to change accepted M1 semantics. | Blocking for affected design section. | Affected contract clause or revision use. | Escalate for human semantic review and keep the choice unresolved. | Technical representation cannot silently amend M1. |

## 21. Synthetic examples

### Example A - Proposal accepted without mutation

Activity revision `R1` is released for candidate activity `ACT-100` with proposed status. Decision revision `D1` is a separate `AnalystDecision` record that references exact `R1`, exact authority basis `AUTH1`, exact context `CTX1`, and accepts the business meaning. The effective view derives accepted for `R1`. The content of `R1` is not mutated.

### Example B - Semantic correction

Revision `R2` keeps the same `record_id` as `R1`, receives a new `revision_id`, supersedes `R1` in `RevisionLineage`, and changes the activity description. The prior acceptance of `R1` does not automatically accept `R2`. `R2` remains proposed or under review until a valid authority basis decides it.

### Example C - Provenance-only correction

Revision `R3` corrects a provenance locator while preserving semantic content. Authority does not transfer implicitly. A later staleness or confirmation policy may define how such cases are confirmed, but that remains [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19). No silent acceptance is inferred.

### Example D - Concurrent branches

Revisions `R2A` and `R2B` both derive from `R1` in the same `RevisionLineage`. Neither silently wins because it has a later creation time or higher confidence. `MULTIPLE_EFFECTIVE_REVISIONS` blocks authoritative use until an explicit merge, rejection, deferral, or authorized decision resolves the branch conflict.

### Example E - Floating reference

A compiler request references only `record_id = ACT-100` and no resolution policy exists. The system emits `FLOATING_REFERENCE_NOT_ALLOWED` and refuses to guess the current revision. The request must identify an exact `revision_id` or use an approved non-authoritative planning mode.

### Example F - Value-state reevaluation

Activity label `Review request` is unchanged from `R1` to `R2`, but evidence revision `EV2` changes whether a system is required. The prior assessment for `R1` used `knowledge_state = known`, `applicability = applicable`, `requirement_state = optional`, and `value_presence = absent` based on `EV1`. Because the evidence basis changed, `R2` cannot inherit the prior four-axis assessment by omission. The system emits `VALUE_STATE_REEVALUATION_REQUIRED` until `R2` has a new assessment or reviewed preservation basis.

### Example G - Cross-record split and derivation

Compound statement revision `S1` says that a request is reviewed and approved. Review meaning and approval meaning are separated into logical records `REC-REVIEW` and `REC-APPROVE`, each with its own initial revision. Both reference exact `S1` through `RecordDerivationGraph`. Neither automatically supersedes `S1`, and no acceptance, context, or value-state assessment transfers automatically.

### Example H - Separate decision and status-basis revision

Activity revision `R1` remains immutable. Decision revision `D1` accepts exact `R1`, so the effective view derives accepted. Later, decision revision `D2` supersedes `D1` and defers the same subject revision. The activity does not become `R2`; the effective view is recomputed from `R1`, `D2`, exact authority, exact context, and exact evidence bases.

### Example I - Invalid preservation assertion

Activity revision `R2` has the same label and payload text as `R1`. The system attempts to preserve the prior four-axis assessment by setting `preserved = true` on `R2`. This is invalid. Preservation requires a separate exact revisioned preservation assertion referencing the predecessor assessment, exact `R2`, both basis sets, exact context, reviewed revision-impact classification, and authority where accepted meaning is affected. The system emits `VALUE_STATE_PRESERVATION_BASIS_INVALID`.

### Example J - External authoritative basis

A target BPMN profile is maintained outside Process IR. A compiler policy references `https://example.invalid/profiles/current`. This is not exact because `current` can change. The basis must instead use an immutable external locator, explicit external version identifier, immutable content identifier, or versioned locator plus integrity descriptor where applicable. The system emits `FLOATING_EXTERNAL_BASIS` until the external profile basis is exact.

### Example K - Historical as-of status replay

An activity revision `R1`, decision revision `D1`, authority basis `AUTH1`, context `CTX1`, and evidence `EV1` form a closed exact basis set as of 2026-07-01. A request asks for historical replay as of that time. The system may derive the historical accepted status from the exact closed basis set, even if later records exist, because the request is explicitly historical/as-of.

### Example L - Current status blocked by unresolved staleness

The same `R1`, `D1`, `AUTH1`, `CTX1`, and `EV1` resolve exactly, but a current-status request is made after evidence `EV2` and context `CTX2` exist. No Accepted Issue #19 staleness policy defines whether the old decision remains current. The system must not infer current accepted status. It returns unresolved with `EFFECTIVE_STATUS_STALENESS_UNDETERMINED`.

## 22. Manual review tests

| Question | Expected answer |
| --- | --- |
| If only the creator field changes while semantic content remains the same, may the system silently rewrite the accepted revision? | No. A new revision is required; authority does not transfer implicitly. |
| If a proposed revision has a digest that matches stored content, does that make it accepted? | No. Digest supports integrity checking, not authority. |
| If an `AnalystDecision` references `record_id` but not exact `revision_id`, can compilation treat it as deciding the current revision? | No. Authoritative decisions must identify exact revisions unless a later accepted policy explicitly permits another behavior. |
| If two branch heads exist for the same logical record, can the system choose the one with later creation time? | No. Branch conflicts remain explicit unless an accepted resolution policy applies. |
| If an Analytical Agent created a revision, does `created_by_actor_ref` authorize acceptance? | No. Authorship and authority are separate. |
| If a new revision changes semantic content, can prior acceptance carry forward automatically? | No under the accepted conservative rule. Controlled confirmation or carry-forward requires a later Accepted policy. |
| If a representation rule appears to narrow accepted M1 semantics, can the contract accept it as a technical detail? | No. It must produce `SEMANTIC_CHANGE_ESCALATION_REQUIRED` and remain unresolved pending review. |
| If the business label is unchanged but the evidence or `SemanticContext` revision changes, may the four-axis assessment be carried forward by omission? | No. A new assessment or explicit reviewed preservation basis is required. |
| Can `knowledge_state` come from `R1`, `applicability` from `R2`, and `value_presence` from `R3` in one effective view? | No. `CROSS_REVISION_VALUE_STATE_COMPOSITION` blocks that unless a later accepted aggregation contract exists. |
| Can a cross-record split be represented as a same-record revision merge? | No. Same-record changes use `RevisionLineage`; cross-record derivation uses `RecordDerivationGraph`. |
| An authorized decision accepting activity revision `R1` is superseded by a deferred decision `D2`. Must the activity become `R2`? | No. `R1` remains immutable. `D2` is a new exact decision revision, and the effective view is recomputed. |
| If a subject revision is exact but its `DecisionAuthorityRef` or `SemanticContext` reference floats to "current", is the effective status reproducible? | No. Every revisioned authoritative basis must resolve exactly. |
| Does assigning a provisional UI identifier make a draft revision immutable? | Not necessarily. The immutable boundary is release through stable `revision_id` plus addressable package inclusion or publication. |
| Can a preservation assertion be a Boolean field on the successor revision? | No. It must be a separate exact revisioned basis record or equivalent exact revisioned semantic record. |
| If the label, payload text, digest, and `record_id` are unchanged, does that preserve the prior four-axis assessment? | No. A valid reviewed preservation assertion or new assessment is required. |
| Can an Analytical Agent authorize preservation when accepted business meaning is affected? | No. The agent may propose preservation, but authority requires exact `DecisionAuthorityRef` unless a later Accepted deterministic policy permits controlled automated confirmation. |
| If an external policy, rule, profile, or authority source uses an unversioned mutable URL, is the basis exact? | No. External authoritative bases need an immutable locator, explicit version, content identifier, or versioned locator plus integrity descriptor where applicable. |
| Does successful resolution of every exact basis revision prove current effective status? | No. Current status also requires a staleness and invalidation policy; otherwise `EFFECTIVE_STATUS_STALENESS_UNDETERMINED` blocks current authoritative result. |
| Can historical/as-of derivation proceed when current status is blocked by unresolved staleness? | Yes, if the request is historical/as-of and uses an exact closed basis set. |

## 23. Open decisions and dependencies

Resolved human-review questions:

- M1.2.1 accepts the conservative no-automatic-authority-carry-forward rule as the machine-readiness default in `REC-CHOICE-005`.
- M1.2.1 accepts revision-scoped four-axis preservation rules in `REC-CHOICE-009`.
- M1.2.1 accepts exact basis requirements across authority, context, evidence, conditions, rules, policies, and external authoritative bases.
- M1.2.1 accepts historical/as-of effective-status derivation and the current-status boundary represented by `EFFECTIVE_STATUS_STALENESS_UNDETERMINED`.
- M1.2.1 accepts the reviewed preservation assertion authority model before any future automated confirmation policy.

Deferred decisions:

- exact identifier syntax,
- timestamp format,
- hash algorithm,
- canonicalization format,
- storage representation,
- serialization technology,
- extension mechanism,
- safe authority carry-forward policy,
- detailed staleness rules,
- replay metadata,
- schema validation.

Dependencies:

- [Issue #17](https://github.com/ThresholdOps/MotiveForce/issues/17) for deterministic replay,
- [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19) for decision staleness and invalidation,
- [Issue #5](https://github.com/ThresholdOps/MotiveForce/issues/5) for machine-readable schema,
- [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20) for mapping-rule and profile propagation,
- [M2](../project-memory/milestones/M2-machine-schema-contract-validation.md) for schema and executable validation.

## 24. Author self-check and human acceptance

### Author self-check

The author may verify only:

- required sections exist,
- terminology is consistent,
- no schema or code was created,
- required diagnostics are present,
- synthetic examples are present,
- manual review tests are present,
- links and Markdown formatting are valid,
- the design-choice classification register exists,
- REV-0002 findings remain materially addressed and are not reopened,
- REV-0003 requested corrections are represented structurally.

Passing author self-check does not constitute semantic or design acceptance.

### Human semantic and design acceptance

Human review evaluated:

- whether accepted M1 semantics were preserved,
- whether immutable released revision semantics are coherent,
- whether exact-reference rules are practical,
- whether authority can leak across revisions,
- whether effective status is deterministic enough conceptually,
- whether `RevisionLineage` and `RecordDerivationGraph` are cleanly separated,
- whether subject and status-basis revisions are cleanly separated,
- whether digest concepts are appropriately limited,
- whether `REC-CHOICE-005` and `REC-CHOICE-009` are acceptable semantic extensions,
- whether the reviewed preservation assertion authority and representation are acceptable,
- whether generalized exact external-basis references are practical,
- whether current effective-status derivation is safely bounded while Issue #19 remains open,
- whether any representation choice is actually a semantic change,
- whether the contract is ready to become `Accepted`.

Final human semantic and design approval is recorded by [REV-0004](../project-memory/reviews/M1-2-1-record-envelope-semantic-design-review-3.md). REV-0002 and REV-0003 findings are closed. The M1.2.1 design, DEC-0005, REC-CHOICE-005, REC-CHOICE-009, generalized external exact-basis rules, and the effective-status boundary are accepted.

This acceptance becomes repository-authoritative through merge of [PR #22](https://github.com/ThresholdOps/MotiveForce/pull/22). The bounded finalization amendment records the supplied human decision and authorized status/governance updates. It does not claim a separate independent full semantic reread of the final amended source head.
