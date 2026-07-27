# AnalystDecision Staleness, Invalidation, Revalidation, and Controlled Authority Carry-Forward Policy

- Project: MøtiveFōrce
- Milestone: M1.2.4
- Status: Accepted
- Scope: Current-authority assessment for exact `AnalystDecision` revisions
- Project status: Concept / pre-MVP

This document is an Accepted semantic and machine-readiness design contract through [REV-0010](../project-memory/reviews/M1-2-4-analyst-decision-staleness-revalidation-review-2.md). Repository-authoritative acceptance becomes effective through merge of PR #25. It is not a machine schema, runtime policy engine, workflow, identity system, persistence model, API, or implementation, and it authorizes no implementation.

## 1. Purpose

An exact `AnalystDecision` can be historically authoritative for its original basis while becoming unusable for a later current-authority request. M1.2.4 defines how that distinction is evaluated without mutating the decision, its subject, or historical provenance.

The contract defines:

- historical or as-of validity separately from current authority,
- an exact `AnalystDecisionBasisSet`,
- four derived current-authority assessment outcomes,
- staleness and invalidation triggers,
- explicit non-triggers,
- exact human revalidation,
- controlled, non-transitive authority carry-forward,
- effective-status, value-state, partial-compilation, and replay boundaries,
- use of inherited diagnostics.

The core rule is:

> Historical authority is a derived authority assessment and preserved provenance fact for an exact original basis. It is not source evidence, does not prove business truth, and does not establish authority for a later current request.

## 2. Accepted basis

This proposal consumes without modifying:

- the accepted [M1 Process IR contract](PROCESS_IR_CONTRACT.md),
- the accepted [M1.2.1 RecordEnvelope contract](PROCESS_IR_RECORD_ENVELOPE_CONTRACT.md),
- the accepted [M1.2.2 Semantic Compiler replay contract](SEMANTIC_COMPILER_REPLAY_CONTRACT.md),
- the accepted [M1.2.3 Diagnostic Policy Contract](PROCESS_IR_DIAGNOSTIC_POLICY_CONTRACT.md),
- accepted [DEC-0005](../project-memory/decisions/DEC-0005-record-envelope-revision-semantics.md),
- accepted [DEC-0006](../project-memory/decisions/DEC-0006-deterministic-semantic-compiler-replay.md),
- accepted [DEC-0007](../project-memory/decisions/DEC-0007-process-ir-diagnostic-severity-aggregation.md),
- M1 `AnalystDecision` and `DecisionAuthorityRef` semantics,
- M1.2.1 subject-revision and status-basis separation,
- the no-automatic-authority-carry-forward default,
- the reviewed four-axis value-state preservation model,
- exact external authoritative-basis requirements,
- the historical/as-of versus current-authority boundary,
- replay exact-basis requirements,
- diagnostic severity, blocking, and aggregation policy.

The accepted contracts remain authoritative. A conflict MUST be escalated rather than silently resolved by this proposal.

## 3. Architectural position

```text
Exact AnalystDecision revision
+ exact original decision basis set
+ exact requested current SemanticContext
+ exact requested as-of time
+ exact candidate current basis set
+ exact staleness-policy revision
        |
        v
AnalystDecision current-authority assessment
        |
        +--> current-authoritative
        +--> revalidation-required
        +--> invalidated-for-current-use
        +--> unresolved
```

The four values are derived assessment outcomes. They are not new M1 lifecycle states and MUST NOT be authored as self-authorizing fields in:

- the subject revision,
- the original `AnalystDecision` revision,
- the `RecordEnvelope`.

A future cached result MAY exist only as a clearly derived artifact that references the exact decision revision, basis closure, requested context, as-of time, staleness-policy revision, result, and diagnostics. This contract defines no cache, storage model, schema, or runtime component.

## 4. Design-choice classification register

| Choice ID | Design choice | Classification | Accepted basis | Rationale | Escalation state |
| --- | --- | --- | --- | --- | --- |
| `STALE-CHOICE-001` | Evaluate historical validity separately from current authority. | M1.2.1-derived | Historical/as-of derivation does not establish current authority. | Preserves provenance without authorizing obsolete meaning. | Accepted by REV-0010. |
| `STALE-CHOICE-002` | Derive current authority for one exact decision, subject, context, operation, policy, and as-of time using exactly four outcomes. | Potential semantic change | M1.2.1 leaves detailed current-authority outcomes to Issue #19. | A determinate outcome model is required before implementation. | Accepted by REV-0010. |
| `STALE-CHOICE-003` | Require an exact closed `AnalystDecisionBasisSet`. | M1.2.1-derived | Authoritative bases must be exact and closed. | Staleness cannot be evaluated against floating dependencies. | Accepted by REV-0010. |
| `STALE-CHOICE-004` | Treat age alone as insufficient to make a decision stale. | Technical representation | Accepted semantics require an exact effective-time or policy basis. | Mere chronology cannot create authority or invalidate it. | Accepted by REV-0010. |
| `STALE-CHOICE-005` | Require revalidation after a materially relevant semantic or contextual basis change. | Potential semantic change | Detailed revalidation triggers were deferred to Issue #19. | Current use must not silently rely on changed meaning. | Accepted by REV-0010. |
| `STALE-CHOICE-006` | Invalidate current use for definite authority, scope, applicability, temporal, or explicit invalidation defects. | M1-derived | `DecisionAuthorityRef` must cover the exact use and effective time. | Definite authority defects cannot be treated as reviewable uncertainty. | Accepted by REV-0010. |
| `STALE-CHOICE-007` | Represent revalidation as a new exact revisioned authority basis, never mutation. | M1.2.1-derived | Released revisions and status bases are immutable and separate. | Preserves the original decision and complete provenance. | Accepted by REV-0010. |
| `STALE-CHOICE-008` | Permit controlled carry-forward only as an explicit, human-authorized, exact, non-transitive revalidation effect. | Potential semantic change | M1.2.1 forbids automatic carry-forward and defers controlled policy. | Bounded confirmation is useful but must not leak authority. | Accepted by REV-0010. |
| `STALE-CHOICE-009` | Treat compiler, mapping, target-profile, rendering, and semantically equivalent BPMN changes as non-triggers by themselves. | M1.2.2-derived | Business authority, compilation, replay, and BPMN validity are separate. | Technical projection changes do not rewrite business meaning. | Accepted by REV-0010. |
| `STALE-CHOICE-010` | Derive unresolved current authority when relevance, impact, lineage, context, or basis cannot be determined. | Potential semantic change | M1.2.1 requires refusal rather than guessed current status. | Uncertainty cannot be converted into current authority. | Accepted by REV-0010. |

All choices are Accepted through REV-0010. `STALE-CHOICE-002`, `STALE-CHOICE-005`, `STALE-CHOICE-008`, and `STALE-CHOICE-010` retain their historical `Potential semantic change` classification because that classification records why explicit human semantic review was required.

## 5. Scope and explicit non-goals

### In scope

- exact decision-basis closure,
- historical/as-of authority evaluation,
- current-authority assessment,
- staleness relevance,
- derived current-use invalidation and explicit invalidation acts,
- human revalidation,
- controlled carry-forward,
- effective-status interaction,
- value-state interaction,
- partial-compilation and replay boundaries,
- inherited diagnostic crosswalk,
- synthetic examples and manual tests.

### Explicit non-goals

- machine schema or programming-language model,
- staleness, rule, workflow, or scheduling engine,
- notification service,
- authentication, IAM, analyst directory, or identity storage,
- persistence, API, transport, UI, or runtime logging,
- executable validation, tests, fixtures, or CI,
- automatic authority agent,
- universal decidability,
- new lifecycle states,
- new diagnostic severity or blocking rules,
- canonical serialization or hashing algorithm.

## 6. Normative terminology

- **Historical validity**: whether an exact decision revision was authoritative within its exact original basis and as-of time.
- **Current authority**: whether that exact decision may be used for one exact requested current subject, context, scope, operation, policy, and as-of time.
- **Original decision basis**: the exact closed set used when the decision became authoritative.
- **Candidate current basis**: the exact closed set relevant to the requested current use.
- **`AnalystDecisionBasisSet`**: conceptual closure identifying every exact basis needed for historical or current-authority evaluation.
- **Staleness trigger**: a relevant change or review condition that prevents current use until human revalidation.
- **Invalidating condition**: a definite defect that removes current authority for an exact scope and time.
- **Revalidation**: a new exact human-authorized basis evaluating the prior decision against a changed exact basis.
- **Controlled carry-forward**: the bounded effect of an exact valid revalidation on named successor revisions; not inheritance.
- **Current-authority assessment**: one derived outcome from the four values defined by this contract.
- **Relevance**: whether a basis change affects the decision subject, meaning, applicability, authority, context, dependencies, or requested operation.
- **Relevance disposition**: an exact, authorized classification of one detected basis change as `relevant`, `not-relevant`, or `undetermined` for one decision and current request.
- **Derived current-use invalidation**: an `invalidated-for-current-use` outcome produced directly from exact bases and exact policy without requiring a newly authored invalidation record.
- **Explicit invalidation or revocation act**: a deliberate authority act represented by a separate exact revisioned status basis or exact superseding decision basis.

Terms such as `latest`, `current`, or `newest` are not exact selectors and MUST NOT determine authority without an accepted resolution basis.

## 7. Historical validity and current authority

### Historical or as-of validity

The historical question is:

> Was the exact `AnalystDecision` revision authoritative within its exact original subject, evidence, context, authority, scope, and effective-time basis?

A decision MAY remain historically valid after it becomes unusable for a later current-authority request. Historical authority is a derived authority assessment and preserved provenance fact for the original exact basis; it is not source evidence and does not prove business truth. Historical invalidity and current invalidity MUST NOT be conflated.

### Current authority

The current question is:

> May the exact `AnalystDecision` revision be used for the exact requested subject revision, process version or variant, `SemanticContext`, organizational scope, operation, and as-of time?

Current authority MUST be derived under an exact staleness-policy revision. Historical replay MUST NOT establish present authority. Current invalidation MUST NOT erase historical provenance or rewrite the prior historical result.

## 8. Exact AnalystDecision basis closure

An authoritative evaluation MUST use an exact `AnalystDecisionBasisSet`.

| Basis concept | Requirement | Purpose |
| --- | --- | --- |
| Analyst decision | Exact `AnalystDecision` revision. | Identifies the decision being evaluated. |
| Subject | Exact subject revision or revisions. | Prevents authority from floating across subject revisions. |
| Evidence | Exact evidence revisions and immutable external evidence references. | Identifies the business basis relied upon. |
| Atomic statements | Exact supporting `AtomicStatement` revisions. | Preserves interpretation provenance. |
| Semantic dependencies | Exact dependent accepted record revisions. | Defines the decision dependency closure. |
| Rules and conditions | Exact rule, condition, and condition-result revisions. | Identifies applicability and requirement basis. |
| Semantic context | Exact `SemanticContext` revision. | Fixes process, version, variant, perspective, organization, scope, and effective time. |
| Authority | Exact `DecisionAuthorityRef`, authority source, scope, effective period, and required attestation basis. | Establishes human authority for the exact use. |
| Status bases | Exact supersession, rejection, deferral, invalidation, and other lifecycle assertion revisions. | Supports effective-status evaluation. |
| Prior decisions | Exact referenced prior decisions. | Preserves decision lineage and conflict basis. |
| Revision impact | Exact impact assessments for relevant successor revisions. | Supports relevance and carry-forward evaluation. |
| Relevance dispositions | Exact disposition for every detected basis change, including changed revisions, affected decision, current subject and context, policy or rule, rationale, scope, authority, and as-of time. | Prevents omitted or unauthorized `not-relevant` classifications from preserving current authority. |
| Value state | Exact four-axis assessments and preservation assertions relied upon. | Prevents silent value-state inheritance. |
| Policy | Exact current-authority and staleness-policy revisions. | Fixes evaluation rules. |
| External bases | Exact immutable external authoritative bases. | Prevents mutable external authority. |
| Request | Exact requested current operation, scope, context, and as-of time. | Defines what is being authorized. |

The basis set MUST NOT use `latest`, `current`, repository `HEAD`, mutable branch names, unversioned mutable URLs, implicit context, implicit authority, omitted dependency selectors, or environment defaults.

The basis set identifies what is evaluated. It is not evidence, authority, acceptance, or current validity by itself.

## 9. Current-authority assessment outcomes

An evaluation MUST derive exactly one of the following conceptual outcomes.

### `current-authoritative`

Derive only when:

- original historical authority was valid,
- all required exact references resolve,
- the decision applies to the exact requested subject revision,
- the requested context, process version, variant, organization, scope, and time are covered,
- authority is valid and effective at the requested time,
- no effective superseding, rejecting, deferring, or invalidating basis removes current authority,
- every detected basis change has an exact authorized relevance disposition,
- every `not-relevant` disposition is derived by a fully applicable Accepted deterministic rule or is human-authorized where material semantic judgment is required,
- no relevance disposition is omitted, unclassified, or `undetermined`,
- no relevant change requires revalidation,
- no conflicting status basis exists,
- every required revalidation or carry-forward basis is exact and valid.

### `revalidation-required`

Derive when:

- the decision remains historically valid,
- a materially relevant basis changed or an exact review condition became active,
- current use requires authorized human review of that changed basis.

This outcome blocks the affected current-authority scope. `STALE_ANALYST_DECISION` applies where its accepted trigger is satisfied. The outcome does not imply that the original decision was historically unauthorized.

### `invalidated-for-current-use`

Derive when a definite invalidating condition exists in exact bases and exact policy or through a valid explicit invalidation or revocation act, including:

- authority expired, was revoked, or is not yet effective,
- authority scope does not cover the requested use,
- requested context, process version, organization, or time is outside the decision,
- an exact effective status basis supersedes or invalidates the decision,
- the decision was never authorized,
- a required authority or status basis is definitively invalid.

Expiry, not-yet-effective authority, scope mismatch, incompatible context, effective-time mismatch, and other exact policy-defined defects are derived current-use invalidations and require no synthetic status record. Deliberate revocation, invalidation, or supersession is an explicit act represented by an exact status basis or superseding decision. Use the inherited specific diagnostic. This contract creates no generic invalidation code.

### `unresolved`

Derive when current authority cannot be determined, including:

- exact references are missing, floating, or unresolved,
- any detected basis change is unclassified or has `undetermined` relevance,
- basis relevance authority or revision impact is unresolved,
- lineage or context applicability is unresolved,
- applicable status bases conflict,
- required basis closure cannot be established,
- the accepted policy does not cover the case.

The system MUST NOT infer current authority.

These outcomes are assessment results, not M1 lifecycle states.

## 10. Conceptual evaluation procedure

Evaluate in this order:

1. Resolve the exact `AnalystDecision` revision.
2. Resolve the exact original decision basis closure.
3. Determine historical or as-of authority within that original basis.
4. Resolve the exact requested current `SemanticContext` and as-of time.
5. Resolve the candidate current subject revision and basis closure.
6. Detect every candidate addition, replacement, supersession, withdrawal, invalidation, expiry, conflict, and context change.
7. Assign each detected change exactly one relevance disposition: `relevant`, `not-relevant`, or `undetermined`.
8. Verify the exact rule or human authority for each relevance disposition.
9. Apply exact revision-impact classifications where applicable.
10. Evaluate current `DecisionAuthorityRef` validity, time, and scope.
11. Evaluate superseding, revalidating, invalidating, rejecting, deferring, and constrain-scope status bases.
12. Derive exactly one current-authority assessment outcome.
13. Recompute effective status from the remaining valid exact status bases.

The procedure MUST NOT choose an outcome using latest timestamp alone, newest record alone, confidence, creator identity, storage order, branch order, compiler success, BPMN Kernel success, or rendering success.

### Relevance disposition and authority

Every detected basis change MUST receive exactly one explicit disposition:

- `relevant`: the change affects the decision or requested current use,
- `not-relevant`: the change is proven not to affect the decision or requested current use,
- `undetermined`: available exact bases and authorized policy cannot establish relevance.

Each disposition MUST identify:

- exact changed basis revisions,
- exact affected `AnalystDecision` revision,
- exact current subject and `SemanticContext`,
- exact policy or rule used,
- relevance rationale and outcome,
- affected and explicitly excluded scope,
- disposition authority,
- applicable as-of time.

The disposition MAY be represented within the exact current-authority assessment basis or by a separate exact revisioned basis record. The exact machine representation remains deferred.

A fully applicable Accepted deterministic rule MAY derive relevance. Material semantic relevance requiring judgment MUST be human-authorized. The Analytical Agent MAY propose a relevance disposition, but MUST NOT authoritatively classify a material change as `not-relevant`. Omission is not `not-relevant`; every unclassified change and every `undetermined` disposition produces `unresolved`. `current-authoritative` requires complete detected-change coverage with no unresolved relevance.

## 11. Staleness and invalidation trigger matrix

### Subject revision

| Change | Current-authority effect |
| --- | --- |
| Same exact subject revision | Passage of time alone creates no staleness; other basis changes may still apply. |
| Semantic-content successor | Prior authority does not transfer. Require a new substantive decision or exact authorized revalidation. |
| Provenance-correction successor | No silent inheritance. Bounded human confirmation may preserve effect only with exact bases, reviewed provenance-only impact, unchanged meaning, compatible context, and sufficient authority. |
| Administrative-metadata successor | Apply the same conservative boundary as provenance correction. |
| Status or authority-basis change | Evaluate the separate changed status or authority basis; do not revise the subject payload. |
| Impact undetermined | Derive `unresolved`; use `REVISION_IMPACT_UNDETERMINED` where applicable. |

### Evidence

| Change | Current-authority effect |
| --- | --- |
| Original evidence superseded but historically valid | Assign an exact relevance disposition. Require revalidation when the successor evidence is `relevant`; derive `unresolved` when relevance is `undetermined`. |
| Evidence withdrawn, invalid, unavailable, or integrity-failed | Derive invalidated or unresolved according to the exact defect. Integrity failure does not itself prove business meaning false. |
| New materially relevant evidence | Require revalidation when an exact authorized `relevant` disposition shows that accepted rules place it in the applicable closure and it supports, contradicts, narrows, broadens, or changes a relied-upon condition. |
| New unrelated evidence | No staleness trigger only after an exact authorized `not-relevant` disposition. Mere repository recency or omission is insufficient. |

### SemanticContext and process version

Revalidation is required when a relied-upon context dimension changes materially, including process version, process variant, perspective, organizational scope, modeled scope, effective-time scope, or another decision basis dimension.

An incompatible context or a request outside authority scope invalidates current use. Authority coverage of a later process version is necessary but not sufficient when relevant semantic meaning changed.

### Dependent semantic records

Every detected change to an exact relied-upon semantic record requires an exact relevance disposition. Revalidation is required when a record is materially revised, superseded, rejected, invalidated, withdrawn, or materially reinterpreted and the disposition is `relevant`. A change outside the decision's applicability and dependency closure is not a trigger only when its exact authorized disposition is `not-relevant`. An unclassified or `undetermined` change produces `unresolved`.

### DecisionAuthorityRef

Current use is derivably invalid when exact bases and exact policy establish that authority expired, is not yet effective, has an invalid source, does not cover the request, or lacks required attestation. A deliberate revocation is an explicit invalidation act and is evaluated from its separate exact status basis.

Replacing an authority reference with a different exact valid authority basis requires a new decision or revalidation basis. The original decision MUST NOT silently retarget itself.

### Decision lineage and status bases

- An effective superseding decision removes the earlier decision from current authority.
- An exact explicit invalidation or revocation act removes current authority only within its stated scope and time.
- Rejection and deferral are evaluated under their exact scope and time.
- Conflicting applicable status bases produce `unresolved`.
- Later creation time alone does not select a winner.

### Time and review conditions

Age alone is not a trigger. A temporal trigger exists only when an exact basis defines authority expiry, decision effective end, review-by date, review condition, process-version retirement, or another accepted temporal rule.

Hard expiry invalidates current use. A review-due condition requires revalidation unless an exact accepted policy defines another result.

## 12. Explicit non-triggers

The following MUST NOT by themselves stale an `AnalystDecision`:

- passage of time without expiry or review condition,
- changed confidence score,
- a new unrelated record,
- unrelated evidence outside the basis closure,
- changed explanation or remediation wording,
- report formatting or diagnostic ordering,
- changed storage location,
- changed runtime, log, trace, or correlation identifier,
- changed compiler build,
- changed BPMN rendering or diagram layout,
- changed target BPMN profile,
- changed mapping rule,
- changed semantically equivalent BPMN representation.

Mapping, profile, compiler, replay, and BPMN validation changes may affect their own authority domains. They do not rewrite accepted business meaning.

## 13. Revalidation representation and authority

An `AnalystDecisionRevalidationBasis` is conceptually either:

- a new exact `AnalystDecision` revision, or
- a separate exact revisioned status-basis record with equivalent authority and provenance semantics.

The exact future schema remains deferred.

Revalidation MUST NOT be:

- a Boolean `revalidated` field,
- mutable metadata on the original decision,
- a status field on the subject revision,
- an Analytical Agent recommendation,
- an inferred compiler or BPMN Kernel result.

Minimum conceptual content:

- exact prior decision revision,
- exact current subject revision or revisions,
- exact original and current basis closures,
- exact current `SemanticContext` and requested as-of time,
- complete detected change set with an exact relevance disposition and authority for every change,
- reviewed revision-impact classifications,
- revalidation rationale and resulting current decision effect,
- exact valid `DecisionAuthorityRef`,
- human actor reference,
- effective time,
- relation to and supersession effect on the prior decision,
- affected and explicitly excluded scopes.

For M1 authority, revalidation MUST be human-authorized. The Analytical Agent MAY identify triggers, compare bases non-authoritatively, recommend revalidation, and prepare questions or evidence summaries. It MUST NOT authoritatively revalidate.

## 14. Controlled authority carry-forward

Controlled carry-forward is an effect of an exact valid revalidation basis. It is not inheritance.

It:

- applies only to exact named successor revisions,
- applies only to exact named context, organization, category, scope, and time,
- originates from one exact named prior decision revision,
- requires exact old and new basis closures,
- requires reviewed revision impact,
- requires human authority covering the new request,
- permits bounded confirmation for provenance-only or administrative change,
- requires substantive review for semantic-content change,
- is non-transitive,
- does not authorize R3 merely because R1-to-R2 was confirmed,
- does not preserve four-axis value state automatically,
- does not establish BPMN validity or mapping eligibility,
- does not authorize another actor, organization, context, or decision category.

Value-state preservation still requires the accepted M1.2.1 preservation basis. No automatic deterministic carry-forward is introduced. Future automated confirmation requires a separate Accepted governance decision.

## 15. Derived invalidation and explicit invalidation acts

### Derived current-use invalidation

A derived current-use invalidation is produced directly from exact bases and exact policy. It includes authority expiry, authority not yet effective, authority-scope mismatch, incompatible current context, decision effective-time mismatch, definitively invalid authority source, or another exact policy-defined invalidating condition.

A derived invalidation does not require a newly authored invalidation record. The assessment MUST reference the exact bases and exact policy that produced `invalidated-for-current-use`. It MUST NOT mutate or delete the original decision, subject revision, historical effective-status result, or historical provenance.

### Explicit invalidation or revocation act

A deliberate invalidation or revocation that changes the applicable status basis MUST be represented by a separate exact revisioned status-basis record or exact superseding decision basis.

The explicit act MUST identify:

- exact affected decision revision,
- exact scope and `SemanticContext`,
- exact effective time,
- reason and exact supporting bases,
- valid authority for the invalidation act,
- relation to a replacement or superseding decision.

An explicit business-authority invalidation MUST be human-authorized unless an already Accepted exact governance policy explicitly supplies that authority. It MUST NOT be a mutable invalidation flag.

Both forms are scoped to current use. Neither means that the historical decision never existed.

## 16. Effective-status derivation

- Only a `current-authoritative` decision may participate as an authoritative current status basis.
- A `revalidation-required` decision MUST NOT authorize current status.
- An `invalidated-for-current-use` decision MUST be excluded from current status bases.
- An `unresolved` decision basis makes the affected current-status derivation unresolved.
- Effective status MUST be recomputed from remaining applicable exact bases.
- A derived invalidation excludes the affected decision by reference to its exact invalidating bases and policy; it does not require a synthetic status record.
- An explicit invalidation act participates through its separate exact status basis.
- Deriving invalidation, applying an explicit act, or removing a basis MUST NOT mutate the subject revision.
- Partial compilation MUST NOT bypass stale, invalidated, or unresolved authority.
- The BPMN Kernel MUST NOT resolve decision staleness or authority.

`EFFECTIVE_STATUS_STALENESS_UNDETERMINED` remains valid when the case is outside accepted policy, relevance is undetermined, required impact classification is absent, exact closure cannot be established, status bases conflict, or another required condition remains unresolved.

This proposal does not claim universal decidability.

## 17. Value-state preservation boundary

Decision revalidation and four-axis value-state preservation are separate authority operations.

- Revalidating an `AnalystDecision` does not preserve `knowledge_state`, `applicability`, `requirement_state`, or `value_presence`.
- Value-state preservation requires its own exact reviewed preservation assertion.
- A missing or stale required value-state assessment makes the dependent decision assessment `unresolved` until the value-state basis is resolved.
- After value-state reevaluation, the resulting changed basis receives its own exact relevance disposition; decision revalidation is required only when that disposition is `relevant`.
- Changed evidence, context, rules, conditions, authority, policy, or semantic payload may require both decision revalidation and value-state reevaluation.
- `impact undetermined` blocks both controlled carry-forward and value-state preservation.
- Neither matching labels nor matching digests prove unchanged four-axis meaning.

## 18. Diagnostic crosswalk

All rows inherit severity `error`, semantic identity, scope-local blocking, aggregation, and ordering from the accepted Diagnostic Policy Contract. M1.2.4 defines trigger boundaries; it does not change accepted code meanings or blocking rules.

| Diagnostic | M1.2.4 trigger boundary | Assessment outcome | Affected scope | Historical use | Remediation authority | Diagnostic-policy relationship |
| --- | --- | --- | --- | --- | --- | --- |
| `STALE_ANALYST_DECISION` | A historically valid material decision has a relevant changed basis or active review condition. | `revalidation-required` | Exact decision and dependent current scope. | May remain valid as-of original basis. | Authorized human revalidation, supersession, rejection, or scoped constraint. | Blocking `error` when emitted for affected current scope. |
| `DECISION_AUTHORITY_REQUIRED` | The exact decision lacks a valid `DecisionAuthorityRef`. A floating or unresolved existing reference uses its inherited exact-reference diagnostic instead. | `invalidated-for-current-use`; historically non-authoritative if the original basis never had valid authority. | Decision and dependent status or compilation scope. | No historical authority exists where original valid authority was absent. | Provide exact valid human authority or treat the decision as non-authoritative. | Inherited blocking rule unchanged; missing authority is not recast as unresolved. |
| `DECISION_AUTHORITY_SCOPE_MISMATCH` | Exact authority does not cover requested subject, category, process, version, organization, context, scope, or time. | `invalidated-for-current-use` | Exact uncovered current request. | Original covered use may remain valid. | New authorized decision, revalidation, or narrower request. | Inherited blocking rule unchanged. |
| `HUMAN_DECISION_REQUIRED` | Current use requires a human decision or revalidation and none exists. | `revalidation-required` | Exact affected current scope. | Historical decision may remain valid. | Authorized human `AnalystDecision` or revalidation. | Inherited blocking rule unchanged. |
| `STALE_REVISION_REFERENCE` | Current use relies on a superseded or invalidated revision, or supersession validity cannot be determined. | `revalidation-required` when review is required; `invalidated-for-current-use` when current use is explicitly invalidated; `unresolved` when supersession or validity cannot be determined. | Exact stale reference and dependents. | Exact historical use may remain valid. | Revalidate, decide, honor exact invalidation, resolve supersession, or intentionally request historical revision. | Inherited current-use blocking rule unchanged. |
| `VALUE_STATE_BASIS_STALE` | Relied-upon value-state assessment has superseded or incompatible exact bases. | `unresolved` until the value-state basis is resolved; after resolution, decision revalidation is considered only if the changed basis is dispositioned `relevant`. | Exact value assessment and dependents. | Prior as-of assessment may remain valid. | Human reevaluation or valid preservation basis, followed by separate decision relevance assessment. | Inherited blocking rule unchanged; value-state repair does not itself decide decision staleness. |
| `VALUE_STATE_REEVALUATION_REQUIRED` | Successor lacks a new assessment or valid preservation assertion after a relevant value-state change. | `unresolved` for the dependent decision assessment until the value-state basis is resolved; `revalidation-required` only after a separate `relevant` decision-basis disposition. | Exact value and dependent decision scope. | Prior assessment remains historical. | Human-reviewed assessment or preservation assertion, then separate decision relevance assessment. | Inherited blocking rule unchanged; value-state reevaluation is not AnalystDecision revalidation. |
| `VALUE_STATE_PRESERVATION_BASIS_INVALID` | Preservation basis is incomplete, unauthorized, mutable, floating, or incompatible. | `unresolved` | Exact preserved-value claim and dependents. | Prior exact assessment may remain historical. | Valid exact human-authorized preservation or reevaluation. | Inherited blocking rule unchanged. |
| `REVISION_IMPACT_UNDETERMINED` | Relevant predecessor-successor impact cannot be classified. | `unresolved` | Exact revisions and dependent authority/value scope. | Historical predecessor remains addressable. | Human impact review or deferral. | Inherited blocking rule unchanged. |
| `EFFECTIVE_STATUS_STALENESS_UNDETERMINED` | Accepted policy cannot establish continued current authority. | `unresolved` | Exact current-status request. | Historical/as-of derivation may proceed. | Complete closure, relevance, impact, or human review. | Inherited current-only blocking rule unchanged. |
| `EFFECTIVE_STATUS_UNRESOLVED` | No single current status derives from exact bases. | `unresolved` | Subject revision and dependent current scope. | Prior as-of status may remain reproducible. | Resolve lineage, authority, context, or status conflict. | Inherited blocking rule unchanged. |
| `CONFLICTING_STATUS_BASIS` | Multiple applicable exact status bases conflict. | `unresolved` | Exact subject, context, and conflicting bases. | Each historical basis remains traceable. | Authorized resolution or split scope. | Inherited blocking rule unchanged. |
| `UNAUTHORIZED_STATUS_BASIS` | Current status relies on authorship, metadata, or invalid authority. | `invalidated-for-current-use` | Exact invalid status basis and dependents. | Historical existence remains traceable, not authoritative. | Correct authority, invalidate basis, and recompute. | Inherited blocking rule unchanged. |
| `STATUS_BASIS_REFERENCE_UNRESOLVED` | Required exact status-basis reference does not resolve. | `unresolved` | Subject and dependent current status. | Closed historical basis may remain valid if independently complete. | Restore or correct exact status basis. | Inherited blocking rule unchanged. |
| `FLOATING_AUTHORITY_BASIS` | Authority uses current/latest or another mutable selector. | `unresolved` | Decision and dependent authoritative operation. | Exact historical authority may remain reproducible. | Resolve authority exactly. | Inherited blocking rule unchanged. |
| `FLOATING_CONTEXT_BASIS` | Context uses a floating selector. | `unresolved` | Exact assertion, decision, status, or compilation scope. | Exact historical context may remain reproducible. | Resolve exact context revision or immutable external basis. | Inherited blocking rule unchanged. |
| `FLOATING_EVIDENCE_BASIS` | Evidence basis floats for authoritative current use. | `unresolved` | Exact assertion, decision, or assessment. | Exact historical evidence may remain reproducible. | Resolve exact evidence or immutable external locator. | Inherited blocking rule unchanged. |
| `FLOATING_EXTERNAL_BASIS` | Any external authority-affecting basis is mutable or unversioned. | `unresolved` | Exact basis set and dependent current output. | Historical use requires its own exact external locator. | Immutable locator, version, content identity, or integrity-bound versioned locator. | Inherited blocking rule unchanged. |

No new diagnostic code is proposed.

## 19. Issue #6 identity boundary

Issue [#6](https://github.com/ThresholdOps/MotiveForce/issues/6) remains responsible for technical analyst identity representation.

M1.2.4 may rely conceptually on a stable `actor_ref`, human actor type, exact `DecisionAuthorityRef`, authority role and scope, and authority effective time. It MUST NOT define identity storage, authentication, IAM, certificates, a private directory, personal-data model, or public-to-private identity mapping.

Issue #6 remains open and not started. Its unresolved technical representation does not block this semantic design.

## 20. Partial-compilation boundary

Issue [#8](https://github.com/ThresholdOps/MotiveForce/issues/8) retains the detailed dependency-closure algorithm.

M1.2.4 defines only that:

- stale, invalidated, and unresolved decisions block the exact current scope that depends on them,
- an independent fragment may proceed only under accepted partial-compilation rules,
- no authoritative fragment may contain stale, invalidated, or unresolved authority in its dependency closure,
- partial compilation MUST NOT hide unresolved current authority.

Issue #8 is not started or completed by this proposal.

## 21. Replay boundary

Historical replay captures, where replayed:

- exact `AnalystDecision` revision and basis closure,
- exact `SemanticContext` and `DecisionAuthorityRef`,
- exact staleness-policy revision,
- exact relevance dispositions and their deterministic-rule or human authority,
- exact evaluation mode and as-of time,
- exact current-authority assessment basis and outcome.

Historical replay MAY reproduce an earlier assessment under its historical policy and basis. It MUST NOT establish present authority. A current evaluation using a different basis or policy is a changed-basis comparison, not same-replay verification.

No Replay Verifier is created.

## 22. Synthetic examples

### Example A - Unchanged exact basis

Decision `D1` and every exact basis remain applicable for the same subject, context, authority scope, and time. The assessment is `current-authoritative`.

### Example B - Time passage alone

Two years pass, but no expiry, review condition, or relevant basis change exists. Age alone does not stale `D1`.

### Example C - Semantic successor

Subject `R2` changes business meaning from `R1`. `D1` accepted exact `R1`; `R2` requires a substantive new decision or revalidation.

### Example D - Provenance-only successor

`R2` corrects provenance only. A human-authorized exact confirmation reviews both closures and may carry `D1` effect to named `R2`.

### Example E - Authority expiry

Authority was valid for the historical decision date but expired before the requested current use. Exact bases and policy derive `invalidated-for-current-use` without requiring a synthetic invalidation record; `D1` remains historically valid.

### Example F - Authority-scope mismatch

`D1` covers process version 3. A request for version 4 is outside scope. Current use is invalidated even if the same actor still exists.

### Example G - Unrelated evidence

New evidence concerns another process. An applicable Accepted deterministic rule or authorized human disposition classifies it exactly as `not-relevant` to `D1`; it creates no staleness trigger. Omission alone would not establish that result.

### Example H - Materially contradictory evidence

New accepted evidence directly contradicts a condition relied upon by `D1`. The current assessment becomes `revalidation-required`.

### Example I - Context variant change

`D1` applies to the standard variant. A regulated variant changes a relied-upon rule. Scoped human revalidation is required.

### Example J - Impact undetermined

`R2` exists, but its impact relative to `R1` is unclassified. Current authority is `unresolved` and `REVISION_IMPACT_UNDETERMINED` applies.

### Example K - Superseding decision

Exact decision `D2` supersedes `D1` for the same scope and effective time. `D1` is excluded from current authority while remaining historical.

### Example L - Conflicting revalidation bases

Two exact applicable revalidation records produce incompatible effects. Current authority is `unresolved` with `CONFLICTING_STATUS_BASIS`.

### Example M - Non-transitive carry-forward

Human confirmation carries `D1` from `R1` to `R2`. A later `R3` is not authorized by that confirmation.

### Example N - Separate value-state preservation

`D1` is considered for `R2`, but the required four-axis assessment is stale. The dependent decision assessment is `unresolved` until value state is reevaluated or validly preserved; the resolved change then receives a separate relevance disposition before deciding whether `D1` requires revalidation.

### Example O - Target-profile change

The target BPMN profile changes while business meaning and decision bases do not. Mapping eligibility may change, but `D1` does not become stale by that fact alone.

### Example P - Historical replay and present invalidation

A replay reproduces the historical accepted result under the old exact basis. Current authority is invalidated because the authority scope later expired. Replay success does not reauthorize it.

## 23. Manual review tests

| Question | Expected answer |
| --- | --- |
| Does a new subject revision inherit an old decision automatically? | No. |
| Does time alone create staleness? | No, absent exact expiry or review condition. |
| May expired authority support current use? | No. |
| May an invalidated decision remain historically valid? | Yes. |
| May the Semantic Compiler or BPMN Kernel revalidate? | No. |
| May the Analytical Agent authoritatively confirm carry-forward or classify a material change as `not-relevant`? | No. |
| May exact human revalidation confirm a provenance-only successor? | Yes. |
| Is controlled carry-forward transitive? | No. |
| Does revalidation mutate the original decision? | No. |
| Does decision revalidation preserve value state automatically? | No. |
| Does unrelated new evidence make a decision stale? | No, after an exact authorized `not-relevant` disposition; omission is insufficient. |
| Does relevant contradictory evidence require revalidation? | Yes. |
| Can modeling policy fix authority-scope mismatch? | No. |
| May partial compilation use stale authority in a fragment closure? | No. |
| Does a changed target profile stale an `AnalystDecision` by itself? | No. |
| Does historical replay prove present authority? | No. |
| Is Issue #6 implementation required for semantic staleness design? | No. |
| May current authority be inferred when relevance is undetermined? | No. |

## 24. Human-review questions

REV-0010 answers all eight human semantic and design review questions `Yes`:

1. Is the separation between historical validity and current authority correct?
2. Are the four current-authority assessment outcomes sufficient?
3. Are the staleness triggers and explicit non-triggers complete and correctly bounded?
4. Is the distinction between `revalidation-required` and `invalidated-for-current-use` correct?
5. Is explicit human-authorized, exact, non-transitive carry-forward sufficiently safe?
6. Is the revalidation and status-basis representation compatible with M1 and M1.2.1?
7. Are effective-status, diagnostic, partial-compilation, identity, and replay boundaries clean?
8. Is the Proposed M1.2.4 design ready for acceptance?

These questions are resolved by the final human semantic and design review.

## 25. Author self-check and human acceptance

### Author self-check

The author may verify:

- required sections and exact basis concepts,
- exactly four assessment outcomes,
- trigger and non-trigger coverage,
- inherited diagnostic references,
- 16 examples and 18 manual tests,
- no mutation, automatic carry-forward, schema, or implementation,
- links, Markdown, IDs, and public-safety constraints.

Author self-check is not human semantic or design acceptance.

### Human semantic and design acceptance

REV-0009 records `Request changes` against reviewed commit `74d288fd57810f0b1a2c7865185889f07e67146e`. Its four bounded corrections address authority/evidence terminology, relevance-disposition authority, derived versus explicit invalidation, and diagnostic-to-outcome fidelity.

[REV-0010](../project-memory/reviews/M1-2-4-analyst-decision-staleness-revalidation-review-2.md) records `Approve` against corrected semantic head `4463aafca5e5fa176bcd3bb0db604b0a48943d9b`, closes `REV9-FIND-001` through `REV9-FIND-004`, accepts `STALE-CHOICE-001` through `STALE-CHOICE-010`, and authorizes merge after bounded finalization validation.

This document is `Accepted`, DEC-0008 is `Accepted`, and M1.2.4 is completed as design-contract work through merge of PR #25. These transitions become repository-authoritative through that merge. No implementation is authorized.
