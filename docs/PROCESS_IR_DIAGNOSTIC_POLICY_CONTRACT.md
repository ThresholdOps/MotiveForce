# Process IR Diagnostic Severity and Aggregation Policy Contract

- Project: MøtiveFōrce
- Milestone: M1.2.3
- Status: Accepted
- Scope: Diagnostic severity, blocking, aggregation, ordering, and outcome derivation
- Project status: Concept / pre-MVP

This document is the semantically accepted M1.2.3 design contract. Final human semantic and design approval is recorded in [REV-0008](../project-memory/reviews/M1-2-3-diagnostic-severity-aggregation-review-2.md), and repository-authoritative acceptance becomes effective through merge of PR #24. It is not a machine schema, diagnostic engine, aggregation engine, validator, runtime logging design, UI specification, or implementation.

## 1. Purpose

The accepted Process IR, RecordEnvelope, and Semantic Compiler replay contracts define diagnostic meanings and blocking conditions but intentionally defer a complete diagnostic policy. M1.2.3 defines the minimum policy needed to make those catalogues sufficiently determinate for later machine representation and implementation.

The policy defines:

- one normative severity vocabulary,
- severity and blocking as separate concepts,
- scope-local and operation-specific blocking,
- a complete registry of accepted diagnostic codes,
- semantic diagnostic identity,
- aggregation, deduplication, and multiplicity,
- deterministic but non-semantic report ordering,
- compilation and replay outcome derivation.

It MUST NOT silently reinterpret an accepted diagnostic meaning or broaden an accepted blocking condition.

## 2. Accepted basis

This contract consumes without modifying:

- the accepted [M1 Process IR contract](PROCESS_IR_CONTRACT.md),
- the accepted [M1.2.1 RecordEnvelope contract](PROCESS_IR_RECORD_ENVELOPE_CONTRACT.md),
- the accepted [M1.2.2 Semantic Compiler replay contract](SEMANTIC_COMPILER_REPLAY_CONTRACT.md),
- accepted [DEC-0005](../project-memory/decisions/DEC-0005-record-envelope-revision-semantics.md),
- accepted [DEC-0006](../project-memory/decisions/DEC-0006-deterministic-semantic-compiler-replay.md),
- M1 compilation outcomes and partial-compilation rules,
- the M1 business-semantic versus modeling-policy boundary,
- M1.2.1 revision, authority, integrity, and current-status boundaries,
- the M1.2.2 semantic diagnostic comparison boundary.

The accepted source contracts remain authoritative. This contract refines only their explicitly deferred diagnostic-policy areas. If a rule conflicts with an accepted source meaning, the source contract controls and the conflict MUST be escalated for human review.

## 3. Architectural position

```text
Accepted diagnostic catalogues
        +
exact evaluated operation and scope
        +
exact diagnostic-policy reference
        |
        v
diagnostic instances
        |
        v
semantic identity + scope-local blocking
        |
        v
deduplicated diagnostic collection
        |
        +--> deterministic non-semantic report view
        |
        +--> compilation or replay outcome derivation
```

This contract defines policy, not an executing component. It does not create a Diagnostic Engine, Aggregation Engine, Replay Verifier, or additional authority layer.

## 4. Design-choice classification register

| Choice ID | Choice | Classification | Accepted basis | Rationale | Escalation state |
| --- | --- | --- | --- | --- | --- |
| `DIAG-CHOICE-001` | Use exactly `error`, `warning`, and `info` as normative severity values. | Potential semantic change | Severity vocabulary was deferred by M1 and M1.2.2. | A small vocabulary separates semantic policy from UI priority while adding a new normative classification. | Resolved and accepted by REV-0008. |
| `DIAG-CHOICE-002` | Treat severity and blocking as separate concepts. | M1-derived | M1 blocking varies by operation and scope. | A defect can remain an error for its own scope while being non-blocking for an independent operation. | Resolved and accepted by REV-0008. |
| `DIAG-CHOICE-003` | Evaluate blocking locally against an exact operation, authoritative scope, and dependency closure. | M1-derived | M1 scope-local refusal and partial compilation. | Global blocking would contradict accepted independent-fragment behavior. | Resolved and accepted by REV-0008. |
| `DIAG-CHOICE-004` | Define semantic diagnostic identity through code, severity, blocking, exact affected records or scope, and semantic parameters. | M1.2.2-derived | Accepted replay diagnostic projection. | Deduplication and replay comparison need the same semantic boundary. | Resolved and accepted by REV-0008. |
| `DIAG-CHOICE-005` | Treat multiplicity as non-semantic by default. | Technical representation | Accepted catalogues define conditions, not count-based escalation. | Repeated emission must not create new authority or stronger blocking. | Resolved and accepted by REV-0008. |
| `DIAG-CHOICE-006` | Define deterministic report ordering as non-semantic. | M1.2.2-derived | Incidental order is outside semantic replay equality. | Stable review output is useful without making order part of meaning. | Resolved and accepted by REV-0008. |
| `DIAG-CHOICE-007` | Derive compilation outcomes from blocking diagnostics intersecting authoritative scope and dependency closure. | M1-derived | Accepted `compiled`, `partially-compiled`, and `refused` rules. | Severity count alone cannot determine semantic completion. | Resolved and accepted by REV-0008. |
| `DIAG-CHOICE-008` | Reproduce normative severity under the exact diagnostic policy during replay. | M1.2.2-derived | Exact diagnostic-policy reference and semantic diagnostic projection. | Same-policy replay must reproduce fields that affect diagnostic meaning. | Resolved and accepted by REV-0008. |
| `DIAG-CHOICE-009` | Do not escalate severity or blocking automatically from diagnostic counts. | Technical representation | No accepted count threshold exists. | Quantity alone does not change the underlying condition or authority. | Resolved and accepted by REV-0008. |
| `DIAG-CHOICE-010` | Keep runtime execution failure distinct from semantic refusal. | M1.2.2-derived | Replay execution failure is separate from semantic outcomes; M1 refusal is valid. | Infrastructure failure does not prove semantic invalidity. | Resolved and accepted by REV-0008. |

`DIAG-CHOICE-001` through `DIAG-CHOICE-010` are accepted by REV-0008. The `Potential semantic change` classification of `DIAG-CHOICE-001` is retained as review provenance for why explicit escalation was required.

## 5. Scope and explicit non-goals

### In scope

- normative severity vocabulary,
- diagnostic-instance blocking evaluation,
- complete accepted-code inventory,
- semantic identity and exact-policy basis,
- aggregation, deduplication, and multiplicity,
- deterministic report ordering,
- derived summaries,
- compilation and replay outcome derivation,
- partial-compilation and replay boundaries,
- synthetic examples and manual review tests.

### Explicit non-goals

- machine schema or programming-language model,
- diagnostic or aggregation engine,
- compiler or Replay Verifier implementation,
- executable validation or test implementation,
- runtime logging or observability,
- API, persistence, database, or UI design,
- hash or identifier algorithm,
- canonical JSON, XML, or other serialization,
- detailed partial-compilation dependency algorithm,
- AnalystDecision staleness trigger policy,
- mapping-rule or target-profile registry,
- new diagnostic codes.

## 6. Normative terminology

- **diagnostic code**: stable identifier whose meaning is defined by an accepted source contract.
- **diagnostic instance**: one occurrence of a diagnostic code evaluated against exact records, scope, parameters, operation, and policy.
- **severity**: normative classification of the condition represented by a diagnostic instance.
- **blocking status**: operation-specific determination that an instance prevents authoritative use of affected scope.
- **authoritative operation**: exact compilation, status derivation, replay verification, mapping, validation, or design-review operation being evaluated.
- **affected scope**: exact semantic scope and exact record revisions to which an instance applies.
- **dependency closure**: exact dependencies required by the evaluated authoritative scope; the detailed partial-compilation algorithm remains Issue #8.
- **semantic parameters**: normalized parameters that determine diagnostic meaning beyond code and affected scope.
- **semantic diagnostic projection**: fields compared for semantic equality and deduplication.
- **semantic duplicate**: diagnostic instance with the same semantic projection as another instance.
- **multiplicity**: number of semantically duplicate contributing occurrences.
- **report order**: deterministic presentation order that does not alter semantic equality.
- **diagnostic policy**: exact policy revision governing severity, blocking, aggregation, ordering, and outcome derivation.

## 7. Normative severity vocabulary

The proposed normative severity values are exactly:

- `error`
- `warning`
- `info`

No `fatal`, `critical`, numeric severity, score-based severity, or UI priority is introduced.

### `error`

An `error` is a semantic, policy, authority, revision, provenance, integrity, or replay defect that invalidates authoritative use of its affected scope, or would invalidate it if that scope were part of the evaluated authoritative operation.

An `error` MAY be non-blocking for the current operation when its exact per-code blocking condition is not active for that operation. This includes an affected value or relation that is not required, an inactive optional or conditional requirement, an integrity check that the operation does not require, or a condition that is provenance-only for that operation. An `error` MAY also be non-blocking when its affected scope is explicitly excluded, historical-only, non-authoritative, or outside the authoritative operation and its relevant dependency closure. It remains an error for its own affected condition.

### `warning`

A `warning` is a material condition requiring attention that does not invalidate authoritative use of the current evaluated scope. A warning MUST NOT be blocking.

### `info`

An `info` diagnostic explains classification, comparison, or normal status and does not represent a defect. An informational diagnostic MUST NOT be blocking.

### Mandatory severity rules

- Every blocking diagnostic instance MUST have severity `error`.
- `warning` and `info` MUST NOT be blocking.
- Severity alone MUST NOT derive compilation or replay outcome.
- Diagnostic count MUST NOT change severity automatically.
- Multiple warnings MUST NOT become an error because of quantity alone.
- Multiple errors MUST NOT create a new severity level.
- Runtime exceptions and infrastructure failures MUST NOT be represented by inventing a higher semantic severity.

All 76 diagnostics inherited from accepted source catalogues describe defects or unmet authoritative conditions in their own affected scopes. Their accepted normative severity is therefore `error`. This contract adds no accepted-code assignment to `warning` or `info`; those values remain available only for later human-reviewed, non-blocking diagnostic definitions.

## 8. Diagnostic instance and blocking semantics

Every diagnostic instance MUST identify:

- diagnostic code,
- severity,
- blocking status,
- affected exact record revisions,
- affected semantic scope,
- operation being evaluated,
- semantic parameters,
- exact diagnostic-policy reference,
- originating source-contract meaning and provenance.

Blocking MUST NOT be inferred solely from severity.

A diagnostic instance is blocking if and only if:

1. the exact per-code blocking condition is satisfied for the evaluated operation;
2. the diagnostic condition exists for the exact instance; and
3. the affected exact records or semantic scope intersect the authoritative operation, or the affected condition belongs to the dependency closure required by that operation.

Blocking is scope-local and operation-specific. An error is non-blocking for the evaluated operation when its exact per-code blocking condition is inactive, even if the affected material is present in a broader operation scope. An error outside the authoritative operation and dependency closure also remains an error but is non-blocking for that operation.

When partial compilation is explicitly enabled, a diagnostic affecting one fragment MUST NOT block an independent fragment when:

- dependency closure is complete,
- the independent fragment contains no blocking diagnostic,
- the result remains `partially-compiled`,
- unresolved and excluded scope remain visible.

This contract does not define the dependency-closure algorithm owned by [Issue #8](https://github.com/ThresholdOps/MotiveForce/issues/8).

## 9. Business-semantic and policy boundary

The accepted distinction remains:

- business-semantic diagnostics require evidence, source clarification, authorized human decision, exclusion, or deferral;
- modeling-policy diagnostics may be resolved only by the applicable modeling decision, profile, mapping policy, or `CompilationPolicyContext`.

The registry also uses authority and governance, revision and provenance, integrity, and replay and verification as review classifications. These are aids, not new authorities.

Mandatory rules:

- `CompilationPolicyContext` MAY resolve only modeling-policy diagnostics.
- Modeling policy MUST NOT resolve business-semantic diagnostics.
- An `AnalystDecision` MUST NOT resolve BPMN legality.
- Category MUST NOT determine severity automatically.
- Category MUST NOT determine blocking automatically.
- Remediation authority MUST remain consistent with accepted source contracts.

## 10. Inventory method and common registry rules

The registry was derived directly from the accepted catalogue tables:

| Source contract | Catalogue rows | Unique codes |
| --- | ---: | ---: |
| M1 Process IR | 35 | 35 |
| M1.2.1 RecordEnvelope | 29 | 29 |
| M1.2.2 Semantic Compiler replay | 12 | 12 |
| **Total** | **76** | **76** |

No source-code duplicates were found. No code is renamed, omitted, or added.

Each registry row preserves the accepted per-code blocking condition. A row that says "when", "only where", "only operation requiring", or otherwise limits blocking MUST be evaluated through the conjunctive rule in section 8; presence of an `error` instance alone MUST NOT make that instance blocking.

Every registry row uses this common semantic identity unless the row adds named parameters:

```text
code
+ severity
+ blocking status
+ affected exact record revisions
+ affected semantic scope
+ semantic parameters
```

Multiplicity is non-semantic for every row. Equal projections MAY be collapsed, but all provenance, evidence, and originating-record references MUST be retained. Counts MUST NOT increase severity, blocking power, or outcome effect.

## 11. Complete diagnostic registry

In the table, "base identity" means the common projection in section 10. "Scope outcome" means the instance affects only the named operation and scope unless its dependency closure intersects another authoritative scope.

### M1 Process IR diagnostics

| Code | Category | Severity | Blocking rule, operation, and scope | Outcome effect | Deduplication identity and multiplicity | Remediation authority and dependencies |
| --- | --- | --- | --- | --- | --- | --- |
| `INSUFFICIENT_EVIDENCE` | Business semantic | `error` | Blocks compilation when the unsupported assertion is required by the evaluated authoritative operation or its closure; non-blocking when that exact requirement is inactive or the assertion is retained only outside that scope. | Refuse affected scope or exclude it under valid partial compilation. | Base identity; multiplicity non-semantic; + assertion, evidence set, and required semantic use. | Evidence, source clarification, scoped exclusion, rejection, or deferral; modeling policy cannot resolve it. |
| `EVIDENCE_REQUIRED` | Business semantic | `error` | Blocks authoritative use of an accepted source-derived assertion lacking evidence. | Refuse or exclude dependent authoritative scope. | Base identity; multiplicity non-semantic; + assertion and required evidence role. | Provide evidence or remove accepted status through valid authority. |
| `MISSING_REQUIRED_INFORMATION` | Business semantic | `error` | Blocks when an applicable required value is absent in evaluated scope or closure. | Refuse affected scope; partial result only outside its closure. | Base identity; multiplicity non-semantic; + value, applicability, requirement, and context. | Evidence-backed value, rule-backed non-applicability, scope reduction, rejection, or deferral. |
| `UNRESOLVED_INTERPRETATION` | Business semantic | `error` | Blocks when interpretation is required for compilation; non-blocking for provenance-only material outside scope. | Refuse or exclude affected semantic use. | Base identity; multiplicity non-semantic; + source value and unresolved interpretation role. | Source clarification, definition, evidence, exclusion, or deferral. |
| `AMBIGUOUS_BUSINESS_MEANING` | Business semantic | `error` | Blocks when multiple plausible interpretations affect compilation or dependency closure. | Refuse or exclude affected scope. | Base identity; multiplicity non-semantic; + exact alternatives and assertion. | Evidence or authorized `AnalystDecision`; policy cannot select business meaning. |
| `CONTRADICTORY_SEQUENCE` | Business semantic | `error` | Blocks scope whose ordering depends on incompatible supported sequence claims. | Refuse or exclude affected flow scope. | Base identity; multiplicity non-semantic; + exact conflicting sequence claims. | Evidence-backed human decision, source correction, or exclusion. |
| `CONTRADICTORY_RESPONSIBILITY` | Business semantic | `error` | Blocks when authoritative role or responsibility is required by scope. | Refuse or exclude affected responsibility scope. | Base identity; multiplicity non-semantic; + exact conflicting assignments. | Evidence and authorized human decision. |
| `AMBIGUOUS_GATEWAY_SEMANTICS` | Business semantic | `error` | Blocks affected branching or merging semantics and dependent mapping. | Refuse or exclude affected gateway scope. | Base identity; multiplicity non-semantic; + alternatives, conditions, and gateway semantic role. | Evidence or authorized human decision. |
| `EQUIVALENT_BPMN_REPRESENTATIONS` | Modeling policy | `error` | Blocks only affected mapping while equivalent representations lack approved policy. | Refuse that mapping; other independent mappings may proceed. | Base identity; multiplicity non-semantic; + semantic meaning and candidate representations. | `ModelingDecision`, mapping policy, or approved profile. |
| `UNRESOLVED_OPTIONALITY` | Business semantic | `error` | Blocks when applicability or requirement affects authoritative scope and conditions are unresolved. | Refuse or exclude affected value or activity scope. | Base identity; multiplicity non-semantic; + subject, condition, applicability, and requirement basis. | Evidence, rule, or authorized human decision. |
| `UNRESOLVED_BUSINESS_CARDINALITY` | Business semantic | `error` | Blocks when unresolved business count or multiplicity affects scope. | Refuse or exclude affected cardinality scope. | Base identity; multiplicity non-semantic; + subject and candidate cardinalities. | Evidence, authorized decision, exclusion, or deferral. |
| `MODELING_MULTIPLICITY_POLICY_REQUIRED` | Modeling policy | `error` | Blocks affected mapping after business cardinality is accepted but representation policy is absent. | Refuse that mapping only. | Base identity; multiplicity non-semantic; + accepted cardinality and representation alternatives. | `ModelingDecision` or approved mapping policy. |
| `UNRESOLVED_EVENT_TRIGGER` | Business semantic | `error` | Blocks event mapping whose trigger meaning is unresolved. | Refuse or exclude affected event scope. | Base identity; multiplicity non-semantic; + event and evidence-backed trigger alternatives. | Evidence or authorized decision; mapping choice cannot bypass meaning. |
| `UNRESOLVED_PARTICIPANT_IDENTITY` | Business semantic | `error` | Blocks when participant or organizational boundary affects compilation or legality. | Refuse or exclude affected participant scope. | Base identity; multiplicity non-semantic; + participant candidates and boundary. | Evidence or authorized human decision. |
| `PARTICIPANT_REPRESENTATION_POLICY_REQUIRED` | Modeling policy | `error` | Blocks affected representation after participant meaning is accepted. | Refuse that representation only. | Base identity; multiplicity non-semantic; + accepted participant meaning and representation alternatives. | `ModelingDecision`, target profile, or mapping policy. |
| `SEMANTIC_CONTEXT_REQUIRED` | Authority and governance | `error` | Blocks context-sensitive authoritative use when no exact or traceably inherited context applies. | Refuse or exclude affected records. | Base identity; multiplicity non-semantic; + record, context requirement, and operation. | Provide exact context or traceable explicit inheritance. |
| `SEMANTIC_CONTEXT_MISMATCH` | Business semantic | `error` | Blocks combined scope or closure containing incompatible contexts, versions, perspectives, variants, organizations, or periods. | Split, refuse, or exclude incompatible scope. | Base identity; multiplicity non-semantic; + exact records and mismatching context dimensions. | Align contexts, split scope, scoped human decision, or exclusion. |
| `DECISION_AUTHORITY_REQUIRED` | Authority and governance | `error` | Blocks use of an authoritative decision without valid exact authority basis. | Refuse dependent status or compilation scope. | Base identity; multiplicity non-semantic; + decision and missing authority role. | Provide valid `DecisionAuthorityRef` or treat decision as non-authoritative. |
| `DECISION_AUTHORITY_SCOPE_MISMATCH` | Authority and governance | `error` | Blocks use when authority scope does not cover exact decision and context. | Refuse dependent status or compilation scope. | Base identity; multiplicity non-semantic; + decision, authority basis, and mismatching scope dimensions. | Correct or replace authority, constrain scope, or obtain authorized decision. |
| `UNRESOLVED_REFERENCE` | Revision and provenance | `error` | Blocks operation whose required referenced record cannot resolve. | Refuse or exclude dependent scope. | Base identity; multiplicity non-semantic; + source reference, target, and dependency role. | Restore or correct reference, or remove dependent mapping. |
| `UNSUPPORTED_MAPPING` | Modeling policy | `error` | Blocks requested mapping outside compiler capability or exact policy. | Refuse affected mapping; independent scope may proceed. | Base identity; multiplicity non-semantic; + requested mapping and capability or policy basis. | Add future support or select supported mapping through review. |
| `MAPPING_NOT_ELIGIBLE` | Modeling policy | `error` | Blocks mapping that fails accepted eligibility conditions for target scope. | Refuse affected mapping. | Base identity; multiplicity non-semantic; + mapping, failed prerequisites, and target profile. | Resolve facts, references, authority, context, or profile prerequisites. |
| `MODELING_POLICY_REQUIRED` | Modeling policy | `error` | Blocks affected compilation or mapping when accepted meaning lacks required policy. | Refuse affected mapping or scope. | Base identity; multiplicity non-semantic; + required policy role and accepted semantic subject. | Approved `CompilationPolicyContext`, `ModelingDecision`, profile, or scope restriction. |
| `TARGET_BPMN_PROFILE_REQUIRED` | Modeling policy | `error` | Blocks compilation eligibility or Kernel validation operation lacking exact target profile. | Refuse affected compilation or validation request. | Base identity; multiplicity non-semantic; + operation and required profile role. | Provide and propagate exact target profile. Trigger details remain Issue #20 where deferred. |
| `TARGET_BPMN_PROFILE_MISMATCH` | Modeling policy | `error` | Blocks pipeline scope using incompatible exact profile bases. | Refuse or split affected mapping or validation scope. | Base identity; multiplicity non-semantic; + exact artifacts and profile identities. | Align profiles, record compatible transformation, or split scope; detailed policy remains Issue #20. |
| `PARTIAL_COMPILATION_POLICY_REQUIRED` | Modeling policy | `error` | Blocks partial-output claim when explicit enablement is absent. | Refuse full requested scope; no partial result. | Base identity; multiplicity non-semantic; + request and missing policy basis. | Explicitly enable partial mode or refuse; detailed closure remains Issue #8. |
| `PARTIAL_COMPILATION_DEPENDENCY_BLOCKED` | Modeling policy | `error` | Blocks proposed fragment whose exact dependency closure contains unresolved or incompatible records. | Exclude fragment or refuse if no authoritative fragment remains. | Base identity; multiplicity non-semantic; + fragment and blocked dependency edges. | Resolve or expand dependencies, or exclude fragment; trigger algorithm remains Issue #8. |
| `HUMAN_DECISION_REQUIRED` | Authority and governance | `error` | Blocks authoritative operation that requires human decision and has none. | Refuse or exclude dependent scope. | Base identity; multiplicity non-semantic; + decision category and affected records. | Evidence-aware `AnalystDecision` with valid authority. |
| `STALE_ANALYST_DECISION` | Authority and governance | `error` | When emitted, blocks use of a material decision in affected current scope; historical use may remain outside current operation. | Refuse current dependent scope. | Base identity; multiplicity non-semantic; + decision, stale basis, context, and effective time. | Reconfirm, supersede, reject, or constrain; trigger policy remains Issue #19. |
| `PROVENANCE_MISSING` | Revision and provenance | `error` | Blocks authoritative use requiring absent evidence, decision, context, or mapping provenance. | Refuse or exclude dependent scope. | Base identity; multiplicity non-semantic; + record and missing provenance role. | Attach exact required provenance through applicable authority. |
| `UNAUTHORIZED_ACCEPTANCE` | Authority and governance | `error` | Blocks use of record marked accepted without valid human authority. | Refuse dependent status or compilation scope. | Base identity; multiplicity non-semantic; + record, claimed status, and invalid authority basis. | Invalidate unauthorized basis and recompute, or add valid decision authority. |
| `RECOMMENDATION_NOT_AUTHORITY` | Authority and governance | `error` | Blocks authoritative use of recommendation as decision basis. | Refuse dependent scope. | Base identity; multiplicity non-semantic; + recommendation and attempted authority role. | Add authorized human decision or keep unresolved. |
| `CONFIDENCE_ONLY_RECOMMENDATION` | Authority and governance | `error` | Blocks use of material recommendation selected solely by confidence. | Refuse recommendation-dependent scope. | Base identity; multiplicity non-semantic; + alternatives, confidence values, and missing rationale. | Add non-confidence rationale or return no recommendation. |
| `PROPOSED_RECORD_NOT_AUTHORITATIVE` | Authority and governance | `error` | Blocks authoritative compilation use of Proposed meaning. | Refuse or exclude proposed-record scope. | Base identity; multiplicity non-semantic; + exact proposed revision and attempted use. | Obtain acceptance or restrict use to non-authoritative diagnostics and planning. |
| `INVALID_VALUE_STATE_COMBINATION` | Business semantic | `error` | Blocks authoritative use when four-axis state is internally inconsistent. | Refuse or exclude affected value scope. | Base identity; multiplicity non-semantic; + exact assessment and all four dimensions. | Correct dimensions or record valid historical/provenance exception. |

### M1.2.1 RecordEnvelope diagnostics

| Code | Category | Severity | Blocking rule, operation, and scope | Outcome effect | Deduplication identity and multiplicity | Remediation authority and dependencies |
| --- | --- | --- | --- | --- | --- | --- |
| `IMMUTABILITY_VIOLATION` | Revision and provenance | `error` | Blocks use of mutated immutable revision and all dependent authoritative scope. | Refuse affected status, package, or compilation use. | Base identity; multiplicity non-semantic; + exact revision and mutation fact. | Restore history and create successor revision. |
| `RELEASED_REVISION_MUTATION` | Revision and provenance | `error` | Blocks altered, erased, or retargeted released revision and dependents. | Refuse dependent operations. | Base identity; multiplicity non-semantic; + released revision and changed content or target. | Restore released revision and express change as successor. |
| `REVISION_REFERENCE_UNRESOLVED` | Revision and provenance | `error` | Blocks authoritative operation requiring unresolved exact `revision_id`. | Refuse or exclude dependent scope. | Base identity; multiplicity non-semantic; + source, target revision, and reference role. | Restore or correct revision, or exclude scope. |
| `REVISION_CYCLE` | Revision and provenance | `error` | Blocks lineage-dependent status, provenance, package, and compilation for cyclic component. | Effective status unresolved; dependent compilation refused. | Base identity; multiplicity non-semantic; + exact cycle edges and record. | Correct lineage references. |
| `INVALID_REVISION_LINEAGE` | Revision and provenance | `error` | Blocks where incompatible same-record lineage affects status or provenance. | Status unresolved or dependent scope refused. | Base identity; multiplicity non-semantic; + exact edge, relation kind, and record identity. | Correct relation or defer. |
| `CROSS_RECORD_REVISION_LINEAGE` | Revision and provenance | `error` | Blocks lineage edge connecting different logical records. | Lineage-dependent use refused. | Base identity; multiplicity non-semantic; + exact edge and both record IDs. | Use derivation graph or valid same-record revisions. |
| `RECORD_DERIVATION_REFERENCE_UNRESOLVED` | Revision and provenance | `error` | Blocks use requiring unresolved exact derivation provenance. | Refuse affected derived-record use. | Base identity; multiplicity non-semantic; + derivation edge, source, target, and role. | Restore or correct exact derivation reference. |
| `INVALID_RECORD_DERIVATION` | Revision and provenance | `error` | Blocks affected use when derivation relation is structurally or semantically incompatible. | Refuse affected derived scope. | Base identity; multiplicity non-semantic; + exact relation, source, target, and incompatibility. | Correct relation, split records, or defer. |
| `MULTIPLE_EFFECTIVE_REVISIONS` | Revision and provenance | `error` | Blocks authoritative use of logical record and context with unresolved candidate heads. | Effective status unresolved; dependent compilation refused. | Base identity; multiplicity non-semantic; + record, context, and candidate revisions. | Merge, decide, defer, or apply later accepted resolution policy. |
| `VALUE_STATE_REEVALUATION_REQUIRED` | Authority and governance | `error` | Blocks authoritative value use lacking new assessment or valid preservation basis. | Refuse affected value and dependents. | Base identity; multiplicity non-semantic; + successor revision and changed bases. | New assessment or reviewed preservation assertion. |
| `VALUE_STATE_BASIS_STALE` | Authority and governance | `error` | Blocks current authoritative use of assessment with superseded or incompatible exact bases. | Refuse current affected value scope. | Base identity; multiplicity non-semantic; + assessment and stale evidence, context, rule, condition, decision, or authority. | Reevaluate or intentionally request historical context; triggers may depend on Issue #19. |
| `CROSS_REVISION_VALUE_STATE_COMPOSITION` | Revision and provenance | `error` | Blocks effective view combining dimensions from different subject revisions without accepted policy. | Effective value unresolved; dependent compilation refused. | Base identity; multiplicity non-semantic; + component assessments and subject revisions. | Use one exact assessment or later accepted aggregation contract. |
| `VALUE_STATE_PRESERVATION_BASIS_INVALID` | Authority and governance | `error` | Blocks reuse of prior assessment when preservation basis is incomplete, unauthorized, mutable, or floating. | Refuse preserved-value claim and dependents. | Base identity; multiplicity non-semantic; + predecessor assessment, successor, both basis sets, context, and impact. | Valid exact reviewed preservation assertion or reevaluation. |
| `FLOATING_REFERENCE_NOT_ALLOWED` | Revision and provenance | `error` | Blocks authoritative use of logical or floating record reference without allowed policy. | Refuse dependent operation. | Base identity; multiplicity non-semantic; + source, logical record, and resolution selector. | Exact `revision_id` or approved non-authoritative resolution policy. |
| `FLOATING_AUTHORITY_BASIS` | Authority and governance | `error` | Blocks status, decision, or compilation scope depending on floating authority basis. | Refuse dependent authoritative operation. | Base identity; multiplicity non-semantic; + authority reference and selector. | Resolve every revisioned authority basis exactly. |
| `FLOATING_CONTEXT_BASIS` | Authority and governance | `error` | Blocks authoritative meaning depending on current/latest context basis. | Refuse affected assertion, status, or compilation scope. | Base identity; multiplicity non-semantic; + context reference and selector. | Exact context revision or immutable external locator. |
| `FLOATING_EVIDENCE_BASIS` | Revision and provenance | `error` | Blocks accepted source-derived use depending on floating evidence. | Refuse affected assertion or assessment. | Base identity; multiplicity non-semantic; + evidence reference and selector. | Exact evidence revision or immutable external locator. |
| `FLOATING_EXTERNAL_BASIS` | Revision and provenance | `error` | Blocks authoritative output depending on mutable external basis. | Refuse affected basis set and output. | Base identity; multiplicity non-semantic; + external locator, basis role, and mutable selector. | Immutable locator, explicit version, content identity, or versioned locator with integrity. |
| `STALE_REVISION_REFERENCE` | Revision and provenance | `error` | When emitted, blocks current authoritative use of stale revision; exact historical use may be non-blocking. | Refuse current dependent scope. | Base identity; multiplicity non-semantic; + source, stale target, context, and use mode. | Revalidate, decide, or intentionally use historical revision; detailed triggers remain Issue #19. |
| `STATUS_BASIS_REFERENCE_UNRESOLVED` | Authority and governance | `error` | Blocks effective-status derivation with unresolved exact status basis. | Status unresolved; dependent compilation refused. | Base identity; multiplicity non-semantic; + subject and missing status-basis reference. | Restore or correct basis revision. |
| `SUBJECT_REVISION_STATUS_MUTATION` | Revision and provenance | `error` | Blocks status derivation or use based on mutated subject payload for status-only change. | Status invalid; dependent use refused. | Base identity; multiplicity non-semantic; + subject revision and attempted status mutation. | Separate status-basis revision and recompute. |
| `REVISION_IMPACT_UNDETERMINED` | Authority and governance | `error` | Blocks preservation, authority carry-forward, and staleness decisions for successor. | Affected status/value unresolved; compilation refused. | Base identity; multiplicity non-semantic; + predecessor, successor, and undetermined change set. | Human review impact or defer; detailed carry-forward remains Issue #19. |
| `EFFECTIVE_STATUS_UNRESOLVED` | Authority and governance | `error` | Blocks authoritative use when no single status derives for exact revision and context. | Dependent compilation refused. | Base identity; multiplicity non-semantic; + subject, context, and status-basis set. | Resolve lineage, authority, context, or basis conflict. |
| `EFFECTIVE_STATUS_STALENESS_UNDETERMINED` | Authority and governance | `error` | Blocks current authoritative status; non-blocking for exact historical/as-of derivation. | Current status unresolved; historical replay may proceed. | Base identity; multiplicity non-semantic; + subject, closed basis, context, effective time, and current/as-of mode. | Return unresolved or perform as-of derivation; trigger and revalidation policy remains Issue #19. |
| `CONFLICTING_STATUS_BASIS` | Authority and governance | `error` | Blocks status operation with conflicting valid-looking exact bases. | Status unresolved; dependent use refused. | Base identity; multiplicity non-semantic; + subject, context, and conflicting basis revisions. | Authorized resolution or split scope. |
| `UNAUTHORIZED_STATUS_BASIS` | Authority and governance | `error` | Blocks status relying on authorship, metadata, or invalid authority. | Status invalid; dependent compilation refused. | Base identity; multiplicity non-semantic; + subject, status claim, and invalid basis. | Correct exact authority basis or invalidate it and recompute. |
| `INTEGRITY_DESCRIPTOR_INCOMPLETE` | Integrity | `error` | Blocks only operation requiring unavailable digest validation; non-blocking where integrity claim is outside operation. | Integrity-dependent use refused. | Base identity; multiplicity non-semantic; + artifact, digest scope, and missing descriptor fields. | Complete descriptor or mark integrity validation unavailable. |
| `INTEGRITY_MISMATCH` | Integrity | `error` | Blocks where exact operation requires failed integrity check. | Refuse affected artifact and dependency closure. | Base identity; multiplicity non-semantic; + artifact, descriptor, expected, and observed integrity result. | Investigate provenance and create corrective revision; never mutate history. |
| `SEMANTIC_CHANGE_ESCALATION_REQUIRED` | Authority and governance | `error` | Blocks acceptance of design section that appears to change accepted semantics. | Affected design remains Proposed and unusable as authority. | Base identity; multiplicity non-semantic; + exact clause, accepted basis, and suspected change. | Human semantic review; technical representation cannot resolve it. |

### M1.2.2 replay diagnostics

| Code | Category | Severity | Blocking rule, operation, and scope | Outcome effect | Deduplication identity and multiplicity | Remediation authority and dependencies |
| --- | --- | --- | --- | --- | --- | --- |
| `REPLAY_INPUT_CLOSURE_INCOMPLETE` | Replay and verification | `error` | Blocks deterministic replay claim for execution or fragment with absent replay-affecting inputs. | `not replayable` for affected comparison. | Base identity; multiplicity non-semantic; + missing dependencies and roles. | Complete exact manifest closure. |
| `FLOATING_REPLAY_DEPENDENCY` | Replay and verification | `error` | Blocks replay output affected by latest/current/mutable selector. | `not replayable`. | Base identity; multiplicity non-semantic; + dependency, role, and selector. | Replace with exact immutable reference or captured value. |
| `REPLAY_DEPENDENCY_UNRESOLVED` | Replay and verification | `error` | Blocks replay when recorded exact dependency cannot resolve. | `not replayable`. | Base identity; multiplicity non-semantic; + dependency identity and role. | Restore exact artifact; no substitution. |
| `COMPILER_IMPLEMENTATION_UNRESOLVED` | Replay and verification | `error` | Blocks same-replay verification when the required compiler implementation or build identity is missing, unavailable, non-immutable, or insufficiently exact. | `not replayable`. | Base identity; multiplicity non-semantic; + compiler identity fields and missing or insufficient element. | Provide immutable implementation, build, dependency, and contract identity. |
| `MAPPING_RULESET_UNRESOLVED` | Replay and verification | `error` | Blocks replay of affected mappings without exact ruleset. | `not replayable`. | Base identity; multiplicity non-semantic; + mapping scope and ruleset basis. | Provide exact ruleset; detailed rules remain Issue #20. |
| `REPLAY_POLICY_UNRESOLVED` | Replay and verification | `error` | Blocks affected output when compilation, diagnostic, normalization, or closure policy is missing or floating. | `not replayable`. | Base identity; multiplicity non-semantic; + policy role and affected output. | Provide exact policy and frozen parameters. |
| `TARGET_PROFILE_BASIS_UNRESOLVED` | Replay and verification | `error` | Blocks requested compilation/model comparison without exact target profile basis. | `not replayable`. | Base identity; multiplicity non-semantic; + profile role and affected scope. | Provide exact profile; detailed compatibility remains Issue #20. |
| `REPLAY_ENVIRONMENT_DEPENDENCY_UNCAPTURED` | Replay and verification | `error` | Blocks execution or fragment whose semantic output depended on uncaptured environment or service. | `not replayable`. | Base identity; multiplicity non-semantic; + environment influence and affected output. | Remove, freeze, or normalize exact influence. |
| `NONDETERMINISTIC_COMPILER_BEHAVIOR` | Replay and verification | `error` | Blocks verification where identical declared complete inputs yield different semantic outcome. | `semantic mismatch` and deterministic claim failure. | Base identity; multiplicity non-semantic; + exact basis and differing semantic projection. | Find hidden influence, correct later implementation, repeat verification. |
| `REPLAY_SEMANTIC_OUTPUT_MISMATCH` | Replay and verification | `error` | Blocks verification when comparable same basis produces different semantic projection. | `semantic mismatch`. | Base identity; multiplicity non-semantic; + exact differing projection fields. | Investigate implementation, closure, and comparison basis. |
| `REPLAY_NOT_COMPARABLE` | Replay and verification | `error` | Blocks same-replay verification when exact compiler, ruleset, policy, profile, or another replay-affecting basis is available for both executions but differs. | `not comparable`; may permit labeled regression comparison. | Base identity; multiplicity non-semantic; + exact original and changed bases. | Restore original basis or classify different comparison. |
| `REPLAY_INTEGRITY_MISMATCH` | Replay and verification | `error` | Blocks replay where required artifact integrity differs. | `not replayable` for affected closure. | Base identity; multiplicity non-semantic; + artifact, descriptor, expected, and observed result. | Retrieve exact artifact and investigate provenance; digest is not authority. |

## 12. Aggregation and deduplication

Aggregation applies to one exact operation under one exact diagnostic-policy revision.

Two instances are semantic duplicates only when their semantic diagnostic projections are equal. The default deduplication key includes:

- code,
- severity,
- blocking status,
- affected exact records or semantic scope,
- semantic parameters.

When duplicates are collapsed, the aggregate MUST:

- retain every contributing provenance and evidence reference,
- retain every originating record reference,
- retain the count only as a derived summary,
- apply the outcome effect once,
- preserve severity,
- preserve blocking status.

The following are not duplicates:

- same code on different exact revisions,
- same code in different semantic scopes,
- same code with different semantic parameters,
- same code with different blocking status,
- same code with different normative severity.

## 13. Multiplicity

Multiplicity is non-semantic by default for every registered code. No accepted source meaning requires count-sensitive semantics.

Multiplicity MAY become semantic only through a later Accepted code-specific policy. M1.2.3 introduces no such rule.

Diagnostic counts:

- MAY be reported as derived summaries,
- MUST NOT create authority,
- MUST NOT increase severity,
- MUST NOT increase blocking power,
- MUST NOT independently change outcome.

## 14. Deterministic non-semantic report ordering

The semantic diagnostic collection is order-independent. When a diagnostic report view is emitted under this exact diagnostic policy, it MUST use:

1. blocking before non-blocking;
2. severity order `error`, `warning`, `info`;
3. diagnostic code in ascending ASCII order;
4. affected semantic-scope stable identifier;
5. affected exact record and revision identifiers in ascending order;
6. semantic parameter names and normalized scalar values in ascending order.

Codes and identifiers used for ordering MUST be exact stable values, not localized labels.

Ordering:

- MUST NOT alter outcome,
- MUST NOT alter semantic identity,
- MUST NOT make equal diagnostic sets unequal,
- MUST NOT require canonical JSON, XML, or byte serialization.

## 15. Compilation outcome derivation

Severity does not directly determine compilation outcome. Diagnostic instances whose exact per-code blocking conditions are active, together with authoritative scope and dependency closure, determine it through the conjunctive blocking rule in section 8.

### `compiled`

The result is `compiled` only when:

- the complete requested scope is in `authoritative_compiled_scope`,
- no blocking diagnostic intersects requested scope, authoritative compiled scope, or required dependency closure.

Warnings, informational diagnostics, and errors that are non-blocking because their exact per-code trigger is inactive or their scope is outside the authoritative operation and dependency closure do not prevent `compiled`.

### `partially-compiled`

The result is `partially-compiled` only when:

- partial compilation is explicitly enabled,
- at least one independent authoritative fragment is produced,
- each authoritative fragment and its closure contain no blocking diagnostic,
- blocking diagnostics remain only in unresolved, excluded, non-authoritative, or independent outside scope,
- incomplete, excluded, and unresolved scope remain visible.

`partially-compiled` MUST NOT be represented as `compiled` or as a complete process.

### `refused`

The result is `refused` when no authoritative compiled scope is produced because blocking semantic, policy, authority, revision, provenance, integrity, or eligibility diagnostics affect the requested authoritative operation.

Refusal is a valid semantic result. Runtime or infrastructure execution failure is not automatically semantic `refused`.

## 16. Replay outcome compatibility

This contract preserves accepted replay outcomes:

- exact semantic match,
- semantic mismatch,
- not replayable,
- not comparable,
- replay execution failed.

Under the same exact diagnostic policy, replay comparison includes:

- code,
- normative severity,
- blocking status,
- affected exact records or semantic scope,
- semantic parameters.

Free text, remediation prose, localization, formatting, timestamps, host or process metadata, logs, traces, correlation IDs, and incidental order remain non-semantic.

When the original and replay executions use the same exact comparable replay basis and the same exact diagnostic policy, both executions complete, and their semantic diagnostic projections differ, the replay result MUST be `semantic mismatch`.

Replay outcome boundaries remain distinct:

- a changed exact policy, compiler, ruleset, profile, or another replay-affecting basis produces `not comparable`;
- a missing, floating, incomplete, or unresolved replay basis produces `not replayable`;
- a runtime execution failure produces `replay execution failed`;
- the same exact comparable basis with unequal semantic projection produces `semantic mismatch`.

This extends the accepted M1.2.2 "at least" projection without creating a separate comparison-policy artifact.

## 17. Deferred Issue boundaries

- [Issue #8](https://github.com/ThresholdOps/MotiveForce/issues/8) owns the detailed partial-compilation dependency-closure algorithm.
- [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19) owns AnalystDecision staleness, invalidation, revalidation, authority expiry, and controlled carry-forward triggers.
- [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20) owns mapping-rule references, target-profile compatibility, and propagation details.
- [Issue #21](https://github.com/ThresholdOps/MotiveForce/issues/21) owns the expanded future contract-test matrix.

For deferred-trigger diagnostics, M1.2.3 defines severity, semantic identity, aggregation, and blocking behavior when emitted. It does not define the missing trigger algorithm. None of Issues #8 or #19-#21 is started by this proposal.

## 18. Derived summaries

A diagnostic collection MAY expose:

- total diagnostic count,
- counts by severity,
- counts by blocking status,
- counts by category,
- counts by affected scope,
- highest present severity,
- whether any blocking diagnostic intersects authoritative scope.

These are derived views. They are not source diagnostics, do not replace the collection, and do not create authority. Highest severity MUST NOT derive compilation outcome independently of blocking scope.

## 19. Synthetic examples

All examples are fictional and public-safe.

### Example A - Blocking error and refusal

`MISSING_REQUIRED_INFORMATION` affects a required value in the requested scope. Partial compilation is disabled. The instance is `error` and blocking, so no authoritative scope is produced and the outcome is `refused`.

### Example B - In-scope error with inactive blocking condition

`INTEGRITY_DESCRIPTOR_INCOMPLETE` affects an artifact present in the evaluated package, but the exact operation does not require digest validation. The instance remains `error` for the incomplete integrity condition but is non-blocking for that operation because its per-code blocking condition is inactive.

### Example C - Warning count

Ten instances classified as `warning` by a future Accepted policy remain warnings. Their count does not create an error or blocking status.

### Example D - Text-only duplicates

Two `PROVENANCE_MISSING` instances have the same code, severity, blocking status, exact record, scope, and semantic parameters. Their explanatory prose differs. They deduplicate, while both origins remain in provenance.

### Example E - Different revisions

`UNRESOLVED_REFERENCE` affects revision `R1` in one instance and revision `R2` in another. They are not duplicates.

### Example F - Different semantic parameters

Two `TARGET_BPMN_PROFILE_MISMATCH` instances affect the same scope but identify different incompatible profiles. They are not duplicates.

### Example G - Independent partial fragment

A blocking `AMBIGUOUS_BUSINESS_MEANING` affects fragment B. Partial compilation is explicitly enabled. Fragment A has complete dependency closure and no blocker, so A may be authoritative while B remains unresolved.

### Example H - Partial remains partial

Fragment A from Example G is produced, but B remains unresolved. The overall outcome is `partially-compiled`, never `compiled`.

### Example I - Ordering is non-semantic

Two reports contain equal diagnostic semantic projections in different presentation order. They are semantically equal.

### Example J - Same-policy severity mismatch

The original replay output records one instance as `error`; the replay records the same code, scope, and parameters as `warning` under the same exact comparable basis and policy. Both executions complete. The semantic diagnostic projections differ, so replay MUST yield `semantic mismatch`.

### Example K - Unresolved versus changed replay basis

One replay request lacks an immutable compiler identity, so `COMPILER_IMPLEMENTATION_UNRESOLVED` makes it `not replayable`. In a separate comparison, both exact compiler identities are available but differ; `REPLAY_NOT_COMPARABLE` makes that comparison `not comparable`. An exact changed diagnostic-policy revision has the same `not comparable` boundary.

### Example L - Runtime failure

An execution host stops before compilation returns a semantic result. This is a runtime execution failure, not semantic `refused`.

## 20. Manual review tests

| Question | Expected answer |
| --- | --- |
| Does severity alone determine whether compilation is refused? | No. |
| Can a warning be blocking? | No. |
| Can an informational diagnostic be blocking? | No. |
| Must a blocking diagnostic have severity error? | Yes. |
| Can an error be non-blocking for the current operation? | Yes. Its exact per-code blocking condition may be inactive even when the affected material is in the broader operation, or its affected scope may be outside the authoritative operation or dependency closure. |
| Do multiple warnings automatically escalate to error? | No. |
| Do duplicate diagnostics increase blocking power? | No. |
| Are two diagnostics with the same code but different exact records duplicates? | No. |
| Does different explanatory prose create a new semantic diagnostic? | No. |
| Does a severity difference under the same exact comparable basis and policy affect replay comparison? | Yes. If both executions complete, the semantic projection difference MUST produce `semantic mismatch`. |
| Does report ordering affect semantic equality? | No. |
| Can partial compilation hide unresolved scope? | No. |
| Can a modeling policy resolve missing business evidence? | No. |
| Does a runtime execution failure equal semantic refusal? | No. |
| Can M1.2.3 define Issue #19 staleness triggers? | No. |
| Can M1.2.3 define the Issue #8 dependency-closure algorithm? | No. |

## 21. Human review conclusions

REV-0008 records affirmative human semantic and design answers to all eight review questions:

1. Is the three-level severity vocabulary sufficient? Yes.
2. Is the separation between severity and blocking correct? Yes.
3. Is the complete per-code registry faithful to accepted M1, M1.2.1, and M1.2.2 semantics? Yes.
4. Are aggregation, deduplication, and multiplicity rules sufficiently determinate? Yes.
5. Is compilation outcome derivation compatible with accepted partial-compilation rules? Yes.
6. Is replay comparison compatible with the accepted M1.2.2 diagnostic projection? Yes.
7. Is deterministic report ordering adequate without making ordering semantic? Yes.
8. Is the design ready for acceptance? Yes.

The three-level vocabulary, severity and blocking separation, 76-code registry, aggregation, deduplication, multiplicity, outcome derivation, replay compatibility, and deterministic non-semantic ordering are accepted.

## 22. Author self-check and human acceptance

### Author self-check

The author may verify:

- all 76 accepted codes are present exactly once,
- no new code was introduced,
- registry columns and policy sections are complete,
- examples and manual tests cover requested behavior,
- accepted source contracts remain unchanged,
- Markdown, links, IDs, and public-safety constraints pass.

Author self-check is not human semantic or design acceptance.

### Human semantic and design acceptance

[REV-0007](../project-memory/reviews/M1-2-3-diagnostic-severity-aggregation-review.md) requested four bounded corrections. [REV-0008](../project-memory/reviews/M1-2-3-diagnostic-severity-aggregation-review-2.md) approves corrected semantic head `fe96e20bf927927fc6fd9e34b9c475b2ad0a1af4`, closes `REV7-FIND-001` through `REV7-FIND-004`, and accepts `DIAG-CHOICE-001` through `DIAG-CHOICE-010`.

This document is `Accepted` for M1.2.3 through merge of PR #24. DEC-0007 is accepted and M1.2.3 is completed as design-contract work through that merge. No schema, implementation, runtime, API, persistence, executable validation, tests, CI, hashing algorithm, or canonical serialization is authorized.
