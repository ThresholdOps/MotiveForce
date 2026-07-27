# Mapping Rule References and Target BPMN Profile Propagation Contract

## 1. Title and status

- Project: MøtiveFōrce
- Milestone: `M1.2.5`
- Contract status: `Proposed`
- Decision record: [DEC-0009](../project-memory/decisions/DEC-0009-mapping-rule-target-profile-propagation.md)
- Tracking Issue: [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20)
- Source branch: `design/m1-2-5-mapping-profile-propagation`
- Base: [`20f53f13938692b9c572b6f9f963e89fc22cb5b8`](https://github.com/ThresholdOps/MotiveForce/commit/20f53f13938692b9c572b6f9f963e89fc22cb5b8)
- Human semantic and design review round 1: [REV-0011](../project-memory/reviews/M1-2-5-mapping-rule-target-profile-propagation-review.md), Request changes
- Human semantic and design re-review: Required under REV-0012
- Acceptance: Not granted
- Merge authorization: Not granted
- Implementation status: Not started

This document is a Proposed semantic and machine-readiness design contract. It is not a machine schema, mapping-rule implementation, rules engine, Semantic Compiler, BPMN Kernel, profile registry, generated metamodel, parser, validator, API, persistence model, UI specification, runtime component, test suite, or CI workflow.

## 2. Purpose

This contract defines the conceptual policy required to make Semantic Compiler mapping decisions:

- exactly identifiable,
- immutable and versioned,
- closed under deterministic replay,
- traceable to exact prerequisites,
- deterministic when multiple semantically eligible rules may apply,
- scoped to one exact target BPMN profile,
- propagated consistently into compiler and Kernel artifacts.

It refines areas explicitly left open by the accepted M1, M1.2.1, M1.2.2, M1.2.3, and M1.2.4 contracts. It does not reinterpret accepted business meaning, authority, replay, diagnostic, partial-compilation, or Kernel boundaries.

## 3. Accepted basis

This proposal consumes without modifying:

- the [M1 Process IR contract](PROCESS_IR_CONTRACT.md),
- the [M1.2.1 RecordEnvelope contract](PROCESS_IR_RECORD_ENVELOPE_CONTRACT.md),
- the [M1.2.2 replay contract](SEMANTIC_COMPILER_REPLAY_CONTRACT.md),
- the [M1.2.3 diagnostic policy](PROCESS_IR_DIAGNOSTIC_POLICY_CONTRACT.md),
- the [M1.2.4 AnalystDecision staleness contract](ANALYST_DECISION_STALENESS_REVALIDATION_CONTRACT.md),
- [DEC-0005](../project-memory/decisions/DEC-0005-record-envelope-revision-semantics.md) through [DEC-0008](../project-memory/decisions/DEC-0008-analyst-decision-staleness-revalidation.md),
- accepted M1 `ProposedBPMNMapping`, `CompilationPolicyContext`, mapping-eligibility, `target_bpmn_profile`, compiler-output, and Kernel authority semantics,
- accepted M1.2.1 exact revision and external-authoritative-basis rules,
- accepted M1.2.2 exact mapping-ruleset, target-profile, and replay-basis rules,
- accepted M1.2.3 severity, blocking, aggregation, and replay diagnostic projection,
- accepted M1.2.4 current-authority assessment rules.

If this proposal appears to conflict with an accepted contract, the apparent conflict is a Potential semantic change requiring human semantic and design review. This document MUST NOT silently supersede an accepted contract.

## 4. Architectural boundary

```text
Accepted semantic records
+ exact current-authority bases
+ exact CompilationPolicyContext
+ exact MappingRulesetRef
+ exact TargetBPMNProfileRef
        |
        v
Mapping-rule applicability evaluation
        |
        +--> satisfied prerequisite records
        +--> blocked or inapplicable candidate rules
        +--> exact selection policy
        |
        v
MappingRuleApplication
        |
        v
CompiledSemanticModel
+ CompilationResult
        |
        v
BPMN Kernel
        |
        v
KernelValidationReport
```

`KernelValidationReport` is the deterministic downstream validation report for one exact `CompiledSemanticModel` and one exact target BPMN profile.

It MUST reference:

- the exact validated `CompiledSemanticModel`,
- the exact `TargetBPMNProfileRef` used by the BPMN Kernel,
- the exact Kernel contract or implementation identity where applicable,
- the validation scope,
- validation findings and outcome,
- profile mismatch or unsupported-feature diagnostics.

It MUST NOT select mapping rules, modify mapping provenance, replace the target profile, reinterpret accepted business meaning, repair a compilation defect, establish business truth, or establish analyst authority.

Successful Kernel validation proves only that the exact compiled semantic model satisfies the exact Kernel validation basis for the declared target profile. It does not prove that source interpretation was correct, evidence was sufficient, an `AnalystDecision` was valid, another target profile would accept the model, or the model is universally BPMN-conformant.

## 5. Design-choice classification

| Choice ID | Proposed choice | Classification | Accepted basis or escalation reason | Status |
| --- | --- | --- | --- | --- |
| `MAP-CHOICE-001` | Separate stable logical mapping-rule identity from immutable rule revision identity. | M1.2.1-derived | Exact logical record and immutable revision semantics apply to revisioned rule bases. | Proposed |
| `MAP-CHOICE-002` | Require `MappingRuleRef` to identify one exact immutable rule revision. | M1.2.1-derived | Authoritative revisioned mapping bases must resolve exactly. | Proposed |
| `MAP-CHOICE-003` | Require `MappingRulesetRef` to close exact membership, imports, replay-affecting policies, and capability requirements without embedding the executing compiler identity. | M1.2.2-derived | Replay already requires one exact mapping-ruleset basis and a separate exact compiler basis. | Proposed |
| `MAP-CHOICE-004` | Treat every membership or imported-ruleset change as a new immutable ruleset revision. | M1.2.1-derived | Released authoritative bases cannot mutate. | Proposed |
| `MAP-CHOICE-005` | Use four exact prerequisite dispositions, require complete candidate coverage, and treat omitted prerequisites or potentially applicable rules as unresolved. | Potential semantic change | M1 defines eligibility requirements but leaves the complete prerequisite and candidate assessment model open. | Proposed |
| `MAP-CHOICE-006` | Require one `MappingEvaluationResult` for every request and create `MappingRuleApplication` only for a rule actually applied. | Potential semantic change | M1 requires mapping provenance but leaves the exact unsuccessful-evaluation artifact and coverage boundary open. | Proposed |
| `MAP-CHOICE-007` | Require deterministic selection among semantically equivalent eligible candidates under an exact accepted policy. | Potential semantic change | M1 allows policy selection among equivalent representations but leaves detailed selection semantics open. | Proposed |
| `MAP-CHOICE-008` | Forbid precedence, priority, or fallback from resolving conflicting business meaning. | M1-derived | Modeling policy cannot resolve business-semantic ambiguity. | Proposed |
| `MAP-CHOICE-009` | Permit generic fallback only when exact rules prove semantic preservation and profile support. | Potential semantic change | M1 forbids downgrading unsupported meaning; a bounded non-degrading fallback requires explicit review. | Proposed |
| `MAP-CHOICE-010` | Require one exact immutable `TargetBPMNProfileRef` for authoritative compilation and validation. | M1.2.1-derived | M1 requires propagation; M1.2.1 requires exact external bases. | Proposed |
| `MAP-CHOICE-011` | Define `ProfileCompatibilityAssessment` as directional, exact, scoped, version-specific, and authorized under an exact governance basis with three outcomes. | Potential semantic change | M1 requires compatible profiles but leaves compatibility semantics and authority open. | Proposed |
| `MAP-CHOICE-012` | Require an explicit immutable `ProfileTransformationBasis` for every profile substitution while forbidding that basis alone from proving semantic preservation. | Potential semantic change | M1 permits explicit compatible transformation but leaves its proof and authority boundary open. | Proposed |
| `MAP-CHOICE-013` | Propagate exact source and target profile provenance across compiler, replay, and Kernel artifacts. | M1-derived | M1 requires the same profile across the pipeline unless explicitly transformed. | Proposed |
| `MAP-CHOICE-014` | Treat every rule, ruleset, policy, compatibility, profile, or transformation change as a changed replay basis. | M1.2.2-derived | Same-replay verification requires the same exact replay-affecting basis. | Proposed |
| `MAP-CHOICE-015` | Limit future deterministic verification and Kernel outputs to their own authority domains. | M1-derived | Compilation, replay comparison, Kernel validation, business truth, and human authority remain separate. | Proposed |

All choices remain Proposed pending human semantic and design review. No classification in this register constitutes acceptance.

## 6. Core terms

- **logical mapping rule**: one conceptual mapping rule across immutable revisions.
- **mapping-rule revision**: one released immutable semantic definition of a logical mapping rule.
- **MappingRuleRef**: an exact reference to one mapping-rule revision and its governing identity basis.
- **mapping ruleset**: an exact closed collection of exact rule revisions, exact imported rulesets, and replay-affecting selection and prerequisite policies.
- **MappingRulesetRef**: an exact immutable reference to one closed ruleset revision.
- **prerequisite**: an exact condition that must receive an explicit disposition for a candidate rule.
- **PrerequisiteSatisfactionRecord**: the exact assessment of one prerequisite against one mapping request and basis.
- **candidate disposition**: an exact result of evaluating one rule revision for one requested mapping scope.
- **MappingEvaluationResult**: the compiler-owned provenance result for every mapping request, including requests that apply no rule.
- **MappingRuleApplication**: the exact compiler-owned record of one selected rule revision being applied to exact inputs under exact policy and profile bases.
- **TargetBPMNProfileRef**: an exact immutable identity for the target BPMN conformance or modeling profile used for mapping and Kernel validation.
- **ProfileCompatibilityAssessment**: an exact directional and scoped assessment between exact profile revisions under an exact policy and authority basis.
- **ProfileTransformationBasis**: the exact basis for producing a new artifact under a different exact target profile.

## 7. MappingRuleRef and rule identity

### 7.1 Logical identity

A logical mapping rule has a stable identity across revisions. Its identity denotes the continuing conceptual rule, not its current content and not a mutable lookup for authoritative use.

A logical rule identifier MUST NOT, by itself, authorize resolution to:

- the latest revision,
- the newest timestamp,
- the repository head,
- the highest version label,
- an environment-selected revision,
- any mutable default.

### 7.2 Exact revision identity

An authoritative `MappingRuleRef` MUST identify one exact immutable rule revision.

Minimum conceptual content:

- stable logical rule identity,
- exact rule revision identity or equivalent immutable external identity,
- explicit rule version where used,
- immutable locator or immutable content identity,
- rule category and exact mapping intent,
- exact input semantic categories,
- exact output BPMN semantic concept or constrained concept set,
- exact prerequisite definitions,
- exact applicability and activation conditions,
- exact target-profile constraints,
- exact capability requirements,
- exact precedence or selection metadata where applicable,
- exact governance or approval basis,
- exact effective-time scope where applicable,
- supersession references,
- integrity descriptor and scope where used.

A human-readable rule name or version label alone is insufficient. Matching integrity metadata proves neither correctness nor authority.

### 7.3 Rule lifecycle and supersession

Released rule revisions are immutable and remain addressable for replay.

Changing any replay-affecting or semantic element creates a new rule revision, including:

- mapping intent,
- source semantic category,
- target BPMN concept,
- prerequisite,
- applicability condition,
- profile constraint,
- capability requirement,
- selection or precedence behavior,
- fallback behavior,
- governance or effective-time basis.

Supersession:

- MUST identify exact predecessor and successor revisions;
- MUST NOT erase the predecessor;
- MUST NOT retarget an existing `MappingRuleRef`;
- MUST NOT make historical replay use the successor;
- does not by itself prove the successor is currently approved;
- does not transfer prerequisite satisfaction or prior mapping eligibility automatically.

A withdrawn or superseded rule remains usable only for an exact historical replay whose recorded historical basis authorizes it. It MUST NOT be silently selected for a new authoritative compilation.

## 8. MappingRulesetRef and exact closure

An authoritative `MappingRulesetRef` identifies one exact immutable ruleset revision and its complete replay-affecting closure.

Minimum conceptual content:

- stable logical ruleset identity,
- exact ruleset revision or equivalent immutable external identity,
- explicit ruleset version where used,
- complete membership of exact `MappingRuleRef` values,
- exact imported `MappingRulesetRef` values,
- import roles and scope,
- exact prerequisite-policy references,
- exact candidate-selection and precedence policy references,
- exact fallback policy references,
- exact target-profile applicability constraints,
- exact compiler capability requirements or predicates where they affect eligibility,
- exact governance or approval basis,
- effective-time scope where applicable,
- supersession references,
- integrity descriptor and scope where used.

### 8.1 Membership

Ruleset membership is semantic and replay-affecting. Adding, removing, replacing, reordering where order is explicitly semantic, or changing the role of a rule creates a new ruleset revision.

Membership MUST identify exact rule revisions. A list of logical rule identifiers, version ranges, mutable package constraints, or latest/current selectors is not an exact ruleset.

### 8.2 Imported rulesets

Every import MUST identify one exact ruleset revision. The closure recursively includes all exact imported memberships and replay-affecting policies.

The closure MUST:

- terminate,
- contain no unresolved import,
- contain no floating import,
- expose duplicate logical-rule revisions and their roles,
- expose conflicting selection or prerequisite policies,
- preserve import provenance,
- be reconstructable for historical replay.

An unresolved, cyclic, floating, or policy-conflicting closure is not an authoritative exact ruleset.

For current mapping or compilation, use the applicable existing compilation diagnostic, including `UNRESOLVED_REFERENCE`, `FLOATING_EXTERNAL_BASIS`, `MODELING_POLICY_REQUIRED`, `MAPPING_NOT_ELIGIBLE`, or `UNSUPPORTED_MAPPING` according to the exact defect. `MAPPING_RULESET_UNRESOLVED` is reserved for replay and verification and MUST NOT classify a current mapping or compilation closure defect.

### 8.3 Ruleset revision

Changing membership, imports, prerequisite policy, selection policy, precedence, fallback, profile constraints, capability constraints, governance basis, or effective-time behavior creates a new immutable ruleset revision.

Two rulesets with identical member digests but different exact policies or profile constraints are not the same ruleset basis.

Rule and ruleset identity may contain exact compiler capability requirements or predicates. It MUST NOT contain the identity of the executing compiler build merely because that build is used for one evaluation.

A changed capability requirement creates a new rule or ruleset revision as applicable. A changed compiler implementation or changed realization of the same requirement changes the exact compiler basis, not the rule or ruleset revision.

## 9. Prerequisite model

Every prerequisite that can affect applicability, eligibility, selection, or output MUST be explicit and exactly referenced.

### 9.1 Prerequisite categories

| Category ID | Category | Required boundary |
| --- | --- | --- |
| `PREREQ-SEMANTIC` | Accepted business semantics | Exact accepted semantic inputs and required business meaning. |
| `PREREQ-AUTHORITY` | Current authority | Exact current-authoritative decisions and status bases required by the mapping. |
| `PREREQ-REFERENCE` | Reference and provenance | Exact resolvable subject, evidence, rule, condition, and provenance references. |
| `PREREQ-VALUE-STATE` | Four-axis value state | Exact applicable value-state assessments or valid preservation bases. |
| `PREREQ-CONTEXT` | Context and applicability | Exact compatible `SemanticContext`, scope, process version, and variant. |
| `PREREQ-MODELING-POLICY` | Modeling policy | Exact `CompilationPolicyContext`, `ModelingDecision`, selection, or representation policy. |
| `PREREQ-PROFILE-CAPABILITY` | Target profile and compiler capability | Exact profile support and exact compiler capability required by the rule. |
| `PREREQ-DEPENDENCY` | Rule and ruleset dependency | Exact required rule, imported ruleset, transformation, and dependency closure. |

Categories classify prerequisites but do not determine authority, severity, or blocking by themselves.

### 9.2 Prerequisite dispositions

Exactly these conceptual dispositions are used:

- `satisfied`: the prerequisite holds for the exact request and basis;
- `not-satisfied`: the prerequisite is applicable and definitively does not hold;
- `unresolved`: the prerequisite cannot be determined from the exact available basis;
- `not-applicable`: an exact accepted rule or authoritative basis establishes that the prerequisite does not apply to the request.

These are conceptual outcomes, not required machine enums.

Omission is not satisfaction and is not `not-applicable`. Every required prerequisite MUST receive exactly one explicit disposition.

`not-applicable` MUST identify the exact condition, rule, context, and authority that establish non-applicability. A default, missing value, absent evidence, empty collection, falsey runtime value, or agent assertion MUST NOT establish `not-applicable`.

### 9.3 PrerequisiteSatisfactionRecord

Minimum conceptual content:

- exact prerequisite identity and revision,
- exact candidate `MappingRuleRef`,
- exact mapping request and affected scope,
- exact semantic input revisions,
- exact current-authority bases,
- exact context,
- exact policy and profile bases,
- exact compiler implementation identity and capability realization where capability is evaluated,
- disposition,
- exact basis supporting the disposition,
- semantic parameters,
- rationale,
- evaluator authority,
- applicable as-of time,
- excluded and unresolved scope,
- diagnostics.

A satisfaction record is immutable once released. It is not evidence, business authority, profile compatibility, or Kernel validation.

### 9.4 Business and modeling-policy separation

Modeling policy MAY satisfy only modeling-policy prerequisites. It MUST NOT satisfy missing business evidence, unresolved business meaning, invalid human authority, stale value state, or incompatible context.

An exact priority, precedence, profile preference, or fallback policy MUST NOT turn a business-semantic prerequisite from `not-satisfied` or `unresolved` into `satisfied`.

## 10. Applicability and candidate dispositions

### 10.1 Candidate enumeration and coverage

Every mapping request MUST be evaluated against the complete exact ruleset closure under an exact candidate-enumeration and filter-policy revision.

For every rule revision in that closure that is potentially applicable to the requested mapping scope, the evaluation MUST record either:

- one of the five candidate dispositions defined below; or
- an exact exclusion basis proving why the rule cannot be a candidate for that request.

An exclusion basis MUST identify the exact rule revision, request, scope, filter-policy revision, exclusion condition, and exact supporting basis. It is not a sixth candidate disposition and MUST NOT be inferred from omission.

If any potentially applicable rule lacks a disposition or exact exclusion basis, candidate coverage is incomplete and the mapping evaluation is `unresolved`. Storage order, discovery order, implementation filtering, or an empty candidate collection MUST NOT establish complete coverage.

### 10.2 Candidate dispositions

Each candidate rule revision evaluated for one exact request receives exactly one conceptual candidate disposition:

- `eligible`: all required prerequisites are satisfied or exactly not applicable;
- `inapplicable`: an exact activation or applicability basis establishes that the rule does not apply;
- `blocked`: one or more applicable prerequisites are not satisfied;
- `unresolved`: applicability or a required prerequisite cannot be determined;
- `not-selected`: the rule was eligible but an exact accepted selection policy selected another semantically equivalent eligible rule.

The candidate-disposition collection MUST expose all considered candidate revisions and their exact bases.

Rules:

- a missing candidate record MUST NOT be treated as inapplicable;
- a known-false activation condition produces `inapplicable`, not `blocked`;
- an unresolved activation condition produces `unresolved`;
- an unsupported required mapping produces `blocked` with `UNSUPPORTED_MAPPING`;
- a rule that fails eligibility MUST NOT be applied;
- an eligible rule is not selected merely because it appears first;
- `not-selected` MUST identify the exact policy and selected alternative;
- no candidate disposition establishes BPMN validity.

### 10.3 MappingEvaluationResult

One conceptual `MappingEvaluationResult` MUST exist for every exact mapping request, including a request that is refused, blocked, unresolved, has no eligible selection, or produces no `MappingRuleApplication`.

Minimum conceptual content:

- stable evaluation identity,
- exact mapping and compilation request,
- requested, affected, excluded, and unresolved scope,
- exact `MappingRulesetRef` and complete ruleset closure,
- exact candidate-enumeration and filter-policy revision,
- complete candidate coverage with every disposition and exact exclusion basis,
- exact prerequisite definitions and all produced `PrerequisiteSatisfactionRecord` values,
- exact semantic input and current-authority bases,
- exact `CompilationPolicyContext` and `TargetBPMNProfileRef`,
- exact selection, precedence, equivalence, and fallback policy bases,
- exact compiler implementation identity and capability realization,
- selected rule or an exact no-selection basis,
- reference to every resulting `MappingRuleApplication`, or an explicit statement that none exists,
- evaluation outcome and relation to `CompilationResult`,
- complete provenance and diagnostics.

Prerequisite and candidate provenance MUST be retained even when no rule is applied. Missing candidate coverage, missing evaluation provenance, or an omitted potentially applicable rule makes the evaluation unresolved; omission MUST NOT produce refusal, inapplicability, or a clean no-selection result by default.

`MappingEvaluationResult` is a conceptual provenance artifact, not a new runtime subsystem, engine, schema, or lifecycle.

## 11. Deterministic selection, precedence, and fallback

### 11.1 Selection basis

Selection occurs only among exact eligible rule revisions that preserve the same accepted business meaning for the same scope and exact target profile.

The selection basis MUST include:

- complete eligible candidate set,
- exact selection-policy revision,
- exact precedence basis where used,
- exact profile basis,
- exact `CompilationPolicyContext`,
- exact semantic-equivalence basis,
- exact tie-resolution rule where needed,
- exact `MappingEvaluationResult` candidate coverage,
- selected rule,
- non-selected eligible rules,
- rationale and diagnostics.

The result MUST be independent of storage order, discovery order, hash-map order, filesystem order, concurrency timing, timestamps, creator identity, and incidental identifier order unless an exact Accepted policy explicitly makes a stable semantic value part of selection.

### 11.2 Equivalent representations

When candidate rules are semantically equivalent and eligible, an exact accepted modeling policy MAY deterministically select one. Without that exact policy, the compiler MUST emit `EQUIVALENT_BPMN_REPRESENTATIONS` and block the affected mapping.

### 11.3 Conflicting candidates

Rules that imply conflicting business meaning are not equivalent candidates. Priority, specificity, ruleset order, profile preference, or compiler capability MUST NOT resolve the conflict.

The compiler MUST preserve the conflict and use the applicable inherited business-semantic diagnostic. Human authority may resolve business meaning only under accepted M1 and M1.2.4 rules.

### 11.4 Precedence

Precedence MAY choose among already eligible semantically equivalent candidates when:

- the precedence policy is exact and accepted,
- its scope covers the request and target profile,
- it defines a deterministic complete result,
- it does not override prerequisites,
- it does not alter accepted business meaning,
- it records all considered candidates and the basis.

Precedence MUST NOT:

- authorize a blocked or unresolved rule,
- replace missing evidence,
- repair stale authority,
- infer profile compatibility,
- change ruleset membership,
- hide excluded or unresolved scope.

### 11.5 Fallback

A fallback rule MAY be applied only when an exact accepted fallback policy establishes all of:

- the fallback preserves the complete accepted business meaning required by the scope;
- every prerequisite is satisfied or exactly not applicable;
- the exact target profile permits the result;
- the compiler capability basis supports it;
- the fallback is explicitly within the ruleset closure;
- provenance identifies the unavailable preferred candidate and fallback basis;
- no unsupported, unresolved, narrowed, or omitted semantic requirement is hidden.

Generic fallback MUST NOT replace unsupported or unresolved business meaning with a generic Task, Event, Gateway, Participant, or other construct. If semantic preservation cannot be established exactly, the mapping is blocked.

## 12. MappingRuleApplication

`MappingRuleApplication` is the exact semantic compiler record that one exact rule revision was selected and actually applied to exact inputs under exact policy and profile bases.

Minimum conceptual content:

- stable application identity,
- exact `MappingEvaluationResult` reference,
- exact compilation request,
- exact mapping scope,
- exact `MappingRuleRef`,
- exact `MappingRulesetRef`,
- exact accepted semantic input revisions,
- exact current-authority bases,
- exact prerequisite definitions and satisfaction records,
- complete candidate-disposition set,
- exact selection and precedence policy,
- exact fallback basis where used,
- exact `CompilationPolicyContext`,
- exact `TargetBPMNProfileRef`,
- exact compiler capability and implementation basis where applicable,
- exact produced or constrained compiled-element identities,
- source, excluded, and unresolved scope,
- mapping provenance,
- diagnostics,
- outcome.

It is distinct from:

- a `ProposedBPMNMapping`,
- a `MappingEvaluationResult`,
- a rule definition,
- a ruleset definition,
- a prerequisite proposal,
- an `AnalystDecision`,
- a `ProfileCompatibilityAssessment`,
- a `KernelValidationReport`.

`MappingRuleApplication` MUST exist only when its exact rule was actually applied. A blocked, refused, unresolved, or no-selection evaluation produces a `MappingEvaluationResult` but no application for a rule that was not applied.

The application MUST NOT mutate its rule, ruleset, inputs, policy, profile, or compiled output. A changed application basis creates a new application and, where output changes, a new compilation outcome.

## 13. TargetBPMNProfileRef

`TargetBPMNProfileRef` is the exact profile identity used for mapping eligibility and downstream Kernel validation.

Minimum conceptual content:

- stable logical profile identity,
- exact profile revision or equivalent immutable external identity,
- explicit profile version where used,
- immutable locator or immutable content identity,
- profile kind or declared profile family,
- exact normative, organizational, or governance basis,
- exact scope of the profile claim,
- exact feature-set or permitted-subset references where available,
- extension-policy basis,
- compatibility-assertion references,
- integrity descriptor where used.

Mandatory rules:

- a profile name alone is insufficient for authoritative identity;
- a version label alone is insufficient when it can identify multiple contents;
- `latest`, `current`, mutable URLs, branch heads, and repository `HEAD` are forbidden;
- changing profile constraints, permitted constructs, extensions, validation rules, or compatibility declarations creates a new exact profile revision;
- historical profile revisions remain addressable for replay;
- exact identity is necessary but does not prove profile correctness;
- integrity metadata is not authority;
- no profile identifier syntax or hash algorithm is selected;
- no runtime profile registry is created;
- no protected BPMN specification content is copied;
- no complete BPMN conformance claim is made.

## 14. Profile compatibility

`ProfileCompatibilityAssessment` is the exact provenance and authority basis for one compatibility determination.

Exactly these conceptual outcomes are used:

- `compatible`,
- `incompatible`,
- `unresolved`.

They are assessment outcomes, not required machine enums.

Minimum conceptual content:

- exact source `TargetBPMNProfileRef`,
- exact target `TargetBPMNProfileRef`,
- direction and exact assessed scope,
- exact compatibility policy, rules, and feature or construct bases,
- assessment outcome,
- evaluator identity and evaluator type,
- exact authority or governance basis for the assessment,
- complete provenance,
- applicable or effective time where relevant,
- diagnostics.

Compatibility MUST be:

- directional,
- specific to exact source and target profile revisions,
- scoped to the exact model, mapping, construct set, feature set, or operation,
- version-specific,
- supported by an exact compatibility basis,
- reproducible under an exact policy revision,
- immutable once released.

```text
Profile A compatible with Profile B
```

does not imply:

```text
Profile B compatible with Profile A
```

Compatibility MUST NOT be inferred solely from similar names, version numbers, profile-family labels, words such as subset or superset, common organization, shared URL, successful XML serialization, validation against a different profile, overlapping constructs, or absence of observed errors in one example.

A model valid under profile A is not automatically valid under profile B.

An exact compatibility relation:

- does not make profile identities equal,
- does not make profiles the same replay basis,
- does not authorize silent substitution,
- does not prove universal model compatibility unless the exact directional and scoped relation explicitly states that claim.

When compatibility cannot be established from exact accepted bases, derive `unresolved`. Derive `incompatible` only when an exact accepted basis establishes incompatibility. No component may guess compatibility.

An Analytical Agent MAY propose a compatibility assessment but its proposal is non-authoritative. The Semantic Compiler MAY derive an authoritative assessment only when a fully applicable Accepted deterministic compatibility policy supplies the exact rules and authority basis.

Model-specific BPMN Kernel validation proves only that one exact model satisfies one exact validation basis. It MUST NOT be promoted into a general profile-to-profile compatibility assertion.

## 15. Explicit profile transformation

The same exact target-profile reference MUST propagate through semantic compilation and validation unless an explicit compatible transformation is recorded.

`ProfileTransformationBasis` minimum conceptual content:

- exact source profile revision,
- exact target profile revision,
- exact source compiled model or affected scope,
- exact transformation-rule or transformation-policy revision,
- exact `ProfileCompatibilityAssessment`,
- explicit semantic-preservation claim,
- exact changed scope,
- exact excluded scope,
- exact unresolved scope,
- source artifact references,
- resulting artifact references,
- complete provenance,
- diagnostics,
- modeling-policy or governance basis,
- effective time where applicable.

Mandatory rules:

- changing only a profile label is not a transformation;
- copying an artifact and changing its profile field is not a transformation;
- the original compiled model remains immutable;
- a transformation produces a new artifact or compilation result;
- any semantic change requires a new compilation outcome;
- narrowed, excluded, unsupported, and unresolved scope remains explicit;
- downstream artifacts retain source and target profile identities;
- the Kernel validates the exact target profile actually used;
- transformation does not establish business truth or human acceptance;
- transformation does not bypass missing prerequisites;
- unsupported business semantics cannot be replaced by a generic construct;
- compatibility requires an exact basis;
- changed transformation basis is a changed replay basis.

`ProfileTransformationBasis` records the claimed transformation basis; it cannot, by itself, establish semantic preservation. Semantic preservation requires the exact accepted semantic inputs, compatibility assessment, transformation rules, mapping policy, authority bases, and evaluation provenance that support the claim.

When a profile transformation changes semantic mapping, it MUST produce a new `MappingEvaluationResult`, each applicable new `MappingRuleApplication`, a new `CompiledSemanticModel`, and a new `CompilationResult`. The original model and application provenance remain immutable.

## 16. Profile propagation matrix

| Artifact | Required target-profile behavior |
| --- | --- |
| `CompilationPolicyContext` | Carries the exact selected `TargetBPMNProfileRef`; no implicit default. |
| Compilation request | References the same exact target-profile revision used to evaluate the request. |
| `ProposedBPMNMapping` | Carries the profile reference where eligibility or representation depends on the profile; remains non-authoritative. |
| `MappingRuleApplication` | References its `MappingEvaluationResult` and records the exact profile used for prerequisite evaluation, applicability, selection, application, and output. |
| `CompiledSemanticModel` | Carries the exact profile governing its semantic mapping result. |
| `CompilationResult` | Carries the same exact profile and reports mapping-evaluation, mismatch, incompatibility, exclusion, or transformation outcomes. |
| `CompilationReplayManifest` | Captures the exact profile revision, `ProfileCompatibilityAssessment`, transformation policy, mapping-evaluation basis, and actual compiler basis where applicable. |
| `KernelValidationReport` | References the exact validated model and exact profile actually used by the Kernel. |

No artifact may silently omit a required target profile, substitute a default, replace an exact revision, widen or narrow scope, infer compatibility, treat a family as an exact profile, or claim validation against a profile different from the one used.

When transformation occurs, the source profile, target profile, transformation basis, affected scope, excluded scope, and replay-affecting basis remain explicit.

## 17. Mapping provenance in compiler outputs

Every authoritative compiled semantic element MUST trace to:

- exact accepted semantic input revisions,
- applicable exact current-authority bases,
- exact `MappingRuleRef`,
- exact `MappingRulesetRef`,
- exact prerequisite satisfaction records,
- exact `MappingEvaluationResult`,
- exact selection, precedence, or equivalent-representation policy,
- exact `TargetBPMNProfileRef`,
- exact `CompilationPolicyContext`,
- exact resulting compiled-element identity.

The combined `CompiledSemanticModel` and `CompilationResult` provenance MUST explain:

- supporting accepted semantic records,
- producing or constraining rule revision,
- containing ruleset revision,
- evaluated prerequisites and dispositions,
- alternative rules considered,
- selection reason,
- governing target profile,
- exact compatibility assessment and authority where applicable,
- profile transformation where applicable,
- excluded and unresolved scope.

Free-text rationale MAY supplement exact provenance. It MUST NOT replace exact rule, ruleset, prerequisite, selection-policy, or profile identity.

## 18. Authority boundaries

### 18.1 Analytical Agent

The Analytical Agent MAY propose BPMN mappings, suggest candidate rules, identify apparently missing prerequisites, compare candidate representations or profiles non-authoritatively, prepare rationale, and recommend a modeling decision.

It MUST NOT make a mapping authoritative, declare eligibility, apply a rule authoritatively, accept business meaning, resolve business ambiguity, classify stale authority as current, authoritatively claim profile compatibility, authoritatively select or transform a profile, or claim BPMN validity.

A `ProposedBPMNMapping` is not a `MappingRuleApplication`.

### 18.2 Semantic Compiler

The Semantic Compiler MAY resolve exact rules and rulesets, produce a complete `MappingEvaluationResult`, evaluate exact prerequisites, determine applicability and eligibility, apply exact rules, select eligible equivalent rules under exact accepted policy, derive profile compatibility under a fully applicable Accepted deterministic policy, emit diagnostics and provenance, and produce `CompiledSemanticModel` and `CompilationResult`.

It MUST NOT reinterpret evidence, resolve business ambiguity, invent missing meaning, treat confidence as authority, use proposed meaning authoritatively, use stale or unresolved current authority, use modeling policy for business prerequisites, silently select or transform a profile, or claim BPMN validity.

### 18.3 BPMN Kernel

The BPMN Kernel MAY validate the exact `CompiledSemanticModel`, apply deterministic BPMN legality and profile validation rules, and emit `KernelValidationReport`.

It MUST NOT choose mapping rules, change ruleset membership, resolve prerequisites, select business mappings, modify provenance, reinterpret business semantics, repair profile mismatch by changing the profile, create `AnalystDecision`, treat successful validation as general profile compatibility, or treat successful validation as business truth.

## 19. M1.2.4 current-authority interaction

A rule MAY consume an `AnalystDecision` only when it is `current-authoritative` for the exact mapping request.

`revalidation-required`, `invalidated-for-current-use`, and `unresolved` decisions block every authoritative mapping whose dependency closure requires them.

A mapping-rule or target-profile change:

- does not by itself stale accepted business meaning,
- may require new mapping-eligibility evaluation,
- may change compiled semantic output,
- changes the replay basis,
- does not inherit prior mapping eligibility.

Controlled carry-forward of an `AnalystDecision` does not carry forward mapping eligibility, rule applicability, prerequisite satisfaction, ruleset selection, or target-profile compatibility. These compiler-policy questions are evaluated independently against exact current bases.

## 20. Replay boundary

Deterministic replay captures, where applicable:

- exact rule revisions,
- exact ruleset revision and complete membership,
- exact imported rulesets,
- exact rule and ruleset capability requirements,
- prerequisite-policy revisions and input bases,
- prerequisite dispositions where part of semantic output,
- selection and precedence policy,
- exact target profile,
- compatibility assertions,
- transformation policy,
- complete `MappingEvaluationResult` provenance,
- mapping-application provenance,
- exact `CompilationPolicyContext`,
- exact compiler implementation identity and actual capability realization.

A changed rule, ruleset, membership, import, prerequisite policy, selection policy, precedence policy, target profile, compatibility basis, or transformation basis is a changed replay basis.

The execution is a regression, migration, compatibility comparison, or new compilation, not verification of the same replay claim. Compatible profiles remain different replay bases.

Historical replay MAY use old exact rulesets and profiles. It does not establish current mapping eligibility, current profile applicability, current rule approval, or current `AnalystDecision` authority.

No Replay Verifier is created.

## 21. Diagnostic crosswalk

All rows inherit severity, blocking, semantic identity, aggregation, ordering, and remediation-authority rules from the [Accepted Diagnostic Policy Contract](PROCESS_IR_DIAGNOSTIC_POLICY_CONTRACT.md). M1.2.5 refines only its owned trigger boundary.

| Diagnostic | Exact M1.2.5 trigger boundary | Affected scope and effect | Remediation authority | Diagnostic-policy and historical boundary |
| --- | --- | --- | --- | --- |
| `UNRESOLVED_REFERENCE` | Required exact rule, ruleset, prerequisite, policy, profile, compatibility, transformation, model, or artifact reference cannot resolve. | Blocks dependent mapping, compilation, or Kernel scope. | Restore or correct exact reference, or exclude dependent scope. | Inherited blocking `error`; exact complete historical closure may remain replayable. |
| `PROVENANCE_MISSING` | Required exact rule, ruleset, prerequisite, selection, profile, transformation, or semantic-input provenance is absent. | Blocks authoritative output lacking required provenance. | Compiler or governing artifact producer must emit exact provenance; business authority is unchanged. | Inherited blocking `error`; complete historical provenance remains valid. |
| `UNSUPPORTED_MAPPING` | Requested mapping lies outside exact compiler capability, ruleset support, or target-profile behavior. | Blocks affected mapping; independent scope follows accepted partial rules. | Add later support or choose a supported semantically preserving mapping under review. | Inherited scope-local blocking `error`; historical supported output may remain replayable. |
| `MAPPING_NOT_ELIGIBLE` | Candidate fails required semantic, authority, reference, value-state, policy, profile, capability, or dependency prerequisites. | Blocks candidate and affected mapping when no eligible candidate remains. | Resolve exact failed prerequisites through their accepted authority domains. | Inherited blocking `error`; prior eligibility does not authorize current request. |
| `MODELING_POLICY_REQUIRED` | Accepted meaning exists but exact modeling, selection, precedence, or representation policy is missing. | Blocks affected mapping or compilation scope. | Authorized modeling policy in `CompilationPolicyContext`; never business evidence. | Inherited blocking `error`; exact historical policy may support historical replay. |
| `EQUIVALENT_BPMN_REPRESENTATIONS` | Multiple semantically equivalent eligible candidates exist without exact accepted selection basis. | Blocks affected mapping until deterministic policy exists. | Authorized modeling decision or accepted selection/profile policy. | Inherited blocking `error`; no effect on accepted business meaning. |
| `MODELING_MULTIPLICITY_POLICY_REQUIRED` | Accepted multiplicity lacks an exact profile-compatible representation policy. | Blocks affected multiplicity mapping. | Authorized modeling policy. | Inherited blocking `error`; does not reopen business cardinality. |
| `PARTICIPANT_REPRESENTATION_POLICY_REQUIRED` | Accepted participant meaning lacks exact profile-compatible pool, lane, black-box, or other representation policy. | Blocks affected participant representation. | Authorized modeling policy or exact profile basis. | Inherited blocking `error`; does not decide participant identity. |
| `TARGET_BPMN_PROFILE_REQUIRED` | Authoritative compilation, eligibility, or Kernel validation lacks an exact target profile. | Blocks affected compilation or validation. | Supply and propagate exact `TargetBPMNProfileRef`. | Inherited blocking `error`; missing profile is not mismatch. |
| `TARGET_BPMN_PROFILE_MISMATCH` | Exact pipeline profiles are incompatible, silently substituted, or misstated. | Blocks affected mapping, compilation, transformation, or validation scope. | Align exact profiles, record exact compatible transformation, or split scope. | Inherited blocking `error`; a changed exact profile is not an unresolved original profile. |
| `MAPPING_RULESET_UNRESOLVED` | During replay or verification, exact ruleset identity, membership, import closure, selection policy, or required historical closure cannot be established. | Replay or verification is `not replayable` for the affected scope. | Restore the complete exact historical ruleset closure. | Replay-only inherited blocking `error`; current mapping closure defects use applicable compilation diagnostics. |
| `REPLAY_POLICY_UNRESOLVED` | Exact prerequisite, selection, compatibility, transformation, or other replay-affecting policy is missing or floating. | Replay is `not replayable` for affected scope. | Supply exact immutable policy basis. | Inherited replay effect; does not authorize policy substitution. |
| `TARGET_PROFILE_BASIS_UNRESOLVED` | Exact target-profile identity or required profile basis cannot resolve for replay or comparison. | Replay is `not replayable`. | Restore exact profile basis. | Inherited blocking `error`; different exact profile uses `REPLAY_NOT_COMPARABLE`. |
| `FLOATING_EXTERNAL_BASIS` | External rule, ruleset, profile, compatibility, transformation, or governance basis uses mutable selector. | Blocks affected authoritative mapping and output. | Provide immutable external locator, version, or content identity. | Inherited blocking `error`; no artificial Process IR revision is required. |
| `FLOATING_REPLAY_DEPENDENCY` | Replay uses current/latest rule, ruleset, profile, compatibility, or transformation basis. | Replay is `not replayable`. | Replace with exact captured basis. | Inherited blocking `error`; historical exact bases remain valid. |
| `REPLAY_NOT_COMPARABLE` | Original and new execution have available exact but different rule, ruleset, policy, profile, compatibility, or transformation bases. | Same-replay verification is `not comparable`; labeled comparison may proceed. | Restore original basis or classify the comparison correctly. | Inherited blocking `error`; changed exact basis is not unresolved. |

No diagnostic code is added, removed, renamed, merged, or reclassified.

## 22. Issue boundaries

### 22.1 Issue #9

[Issue #9](https://github.com/ThresholdOps/MotiveForce/issues/9) retains BPMN metamodel-generation strategy, normative source handling, generated coverage, XSD/CMOF transformation strategy, licensing, future conformance coverage, and conformance tests.

M1.2.5 defines only exact profile identity, immutable external bases, compatibility, propagation, and mapping/profile provenance.

It does not define generated BPMN classes, generation code, parser or Kernel implementation, complete BPMN coverage, copied protected specification content, or conformance claims.

Issue #9 remains open and not started. It does not block this bounded identity, reference, compatibility, and propagation design.

### 22.2 Issue #8

[Issue #8](https://github.com/ThresholdOps/MotiveForce/issues/8) retains detailed partial-compilation dependency-closure policy.

M1.2.5 defines only that unresolved or blocking rules, rulesets, imports, prerequisites, selection policies, profiles, compatibility bases, transformations, and mapping applications block exact affected scope and dependent fragments.

An independent fragment may proceed only under accepted partial-compilation rules. Partial compilation cannot hide an unresolved ruleset, prerequisite, profile mismatch, unsupported required mapping, or stale authority.

Issue #8 remains open and not started.

### 22.3 Issue #21

[Issue #21](https://github.com/ThresholdOps/MotiveForce/issues/21) retains the expanded executable contract-test matrix.

This proposal includes synthetic examples and manual review tests only. It creates no fixture, executable test, validator, or CI workflow.

Issue #21 remains open and not started.

## 23. Synthetic examples

### Example 1 - Exact rule and ruleset

Ruleset `RS1@4` contains exact rule `RULE-A@7`. Complete candidate enumeration records every potentially applicable rule or exact exclusion basis. All prerequisites are satisfied under profile `P1@3`; the compiler records one `MappingEvaluationResult`, one `MappingRuleApplication`, and complete provenance.

### Example 2 - Floating ruleset

A request uses `ruleset/latest`. The compiler emits `FLOATING_EXTERNAL_BASIS` or `FLOATING_REPLAY_DEPENDENCY` according to the operation and blocks authoritative use.

### Example 3 - Rule content change

`RULE-A@7` maps accepted meaning to one concept. A prerequisite changes. The change is released as `RULE-A@8`; `RULE-A@7` remains addressable.

### Example 4 - Membership change

`RULE-B@2` is added to `RS1@4`. The resulting ruleset is `RS1@5`; `RS1@4` is not mutated.

### Example 5 - Unresolved prerequisite

A required authority basis cannot resolve. The prerequisite and candidate dispositions are `unresolved`. The `MappingEvaluationResult` preserves the complete unsuccessful evaluation and no `MappingRuleApplication` is emitted.

### Example 6 - False activation condition

An exact accepted condition proves a rule does not apply to variant `V2`. Its candidate disposition is `inapplicable`, not blocked.

### Example 7 - Modeling policy and evidence

A rule requires an evidence-backed event trigger. A modeling preference exists, but evidence is missing. The business prerequisite remains not satisfied.

### Example 8 - Equivalent candidates

Two eligible rules preserve the same accepted meaning. Without exact selection policy, `EQUIVALENT_BPMN_REPRESENTATIONS` blocks the mapping.

### Example 9 - Conflicting candidates

Two candidates imply different business sequencing. Priority does not choose between them; business meaning remains unresolved.

### Example 10 - Profile-specific precedence

Two equivalent candidates are eligible. Exact accepted profile policy selects the one permitted by `P1@3`; the other becomes `not-selected`. Every other potentially applicable ruleset member has an exact candidate disposition or exclusion basis.

### Example 11 - Invalid generic fallback

A preferred mapping is unsupported. A generic task would omit accepted event semantics, so fallback is forbidden and `UNSUPPORTED_MAPPING` blocks the scope.

### Example 12 - Missing target profile

The request supplies no exact target profile. `TARGET_BPMN_PROFILE_REQUIRED` blocks authoritative compilation.

### Example 13 - Profile mismatch

The model records `P1@3`, but the Kernel request declares incompatible `P2@1`. `TARGET_BPMN_PROFILE_MISMATCH` blocks validation.

### Example 14 - Directional compatibility

An exact `ProfileCompatibilityAssessment` under an Accepted deterministic policy says a model scope from `P-NARROW@2` is compatible with `P-WIDE@5`. It records direction, scope, evaluator, authority, provenance, time, and diagnostics. No reverse compatibility is inferred.

### Example 15 - Compatible profiles and replay

`P1@3` and `P2@1` are exactly compatible for one scope. They remain different replay bases; changing from one to the other is not same-replay verification.

### Example 16 - Explicit profile transformation

A semantic-changing transformation from `P1@3` to `P2@1` records both profiles, exact policy, compatibility assessment, changed and excluded scope, and the supporting semantic-preservation bases. It produces a new mapping evaluation, application, compiled model, and compilation result; `ProfileTransformationBasis` alone is insufficient.

### Example 17 - Silent profile replacement

A copied model changes only its profile field from `P1@3` to `P2@1`. No transformation basis exists. The artifact is invalid for authoritative use.

### Example 18 - End-to-end provenance

A compiled element identifies exact semantic input `R7`, decision basis `D4`, mapping evaluation, rule `RULE-A@7`, ruleset `RS1@4`, prerequisite records, profile and compatibility bases `P1@3`, actual compiler identity, and the Kernel report that validates the resulting model.

### Example 19 - Historical replay

An old exact ruleset and profile are superseded but still available. Historical replay reproduces the prior output without establishing current eligibility.

### Example 20 - Changed ruleset comparison

Original execution uses `RS1@4`; new execution uses exact `RS1@5`. `REPLAY_NOT_COMPARABLE` classifies same-replay verification as not comparable.

### Example 21 - Profile change and business authority

The target profile changes while accepted business meaning does not. The `AnalystDecision` is not stale solely for that reason, but mapping eligibility is reevaluated.

### Example 22 - Unresolved ruleset import

`RS1@4` imports exact `RS-COMMON@9`, but that revision is unavailable. Current compilation emits `UNRESOLVED_REFERENCE` and blocks affected scope. A replay whose required historical ruleset closure cannot be reconstructed emits `MAPPING_RULESET_UNRESOLVED` and is `not replayable`.

## 24. Manual review tests

| Question | Expected answer |
| --- | --- |
| May a version label alone identify a rule exactly? | No. |
| May a ruleset reference use `latest`? | No. |
| Does changing membership or capability requirements require a new ruleset revision while changing only the executing compiler changes the compiler basis? | Yes. |
| May storage order select a mapping rule? | No. |
| May omission of a prerequisite or potentially applicable rule mean satisfied, inapplicable, or cleanly excluded? | No; omission makes the evaluation unresolved. |
| Does `not-applicable` require an exact basis? | Yes. |
| Can modeling policy satisfy missing business evidence? | No. |
| Can the Analytical Agent authoritatively apply a mapping rule or establish profile compatibility? | No. |
| Can the compiler resolve business ambiguity using rule precedence? | No. |
| Can a ruleset select among equivalent eligible mappings under an exact policy? | Yes. |
| Can generic fallback hide unsupported or unresolved semantics? | No. |
| Is an exact target profile required for authoritative compilation? | Yes. |
| May a profile name alone establish exact profile identity? | No. |
| Is profile compatibility directional? | Yes. |
| Does compatibility make two profiles the same replay basis? | No. |
| May a pipeline artifact silently replace the target profile? | No. |
| Can `ProfileTransformationBasis` alone prove semantic preservation or mutate the original model? | No. |
| Must `KernelValidationReport` record the exact profile actually validated? | Yes. |
| Does a changed mapping rule stale accepted business meaning by itself? | No. |
| Is `MAPPING_RULESET_UNRESOLVED` used for current compilation closure defects or a changed exact replay basis? | No; it is replay-only, while current defects use compilation diagnostics and changed exact bases use `REPLAY_NOT_COMPARABLE`. |
| Does successful model-specific Kernel validation establish general profile compatibility or business correctness? | No. |
| Does M1.2.5 implement a profile registry or BPMN metamodel? | No. |
| Can Issue #9 remain deferred while exact reference semantics are designed? | Yes. |
| Can partial compilation hide an unresolved target profile? | No. |

## 25. Human-review questions

1. Are logical rule identity, immutable rule revision, and exact ruleset closure correctly separated?
2. Are rule prerequisites and prerequisite-satisfaction semantics sufficiently complete?
3. Is `MappingRuleApplication` correctly separated from agent proposals, rule definitions, and Kernel validation?
4. Are multi-rule applicability, precedence, fallback, and equivalent-representation rules safely bounded?
5. Are exact target-profile identity, directional compatibility, and explicit transformation semantics correct?
6. Is target-profile propagation across compiler, replay, and Kernel artifacts complete?
7. Are authority, diagnostic, Issue #9, partial-compilation, and replay boundaries clean?
8. Is the Proposed M1.2.5 design ready for acceptance?

No question is answered as Accepted in this Draft delivery.

## 26. Acceptance boundary

This contract remains Proposed until:

- human semantic and design review evaluates the eight questions,
- every Potential semantic change receives an explicit disposition,
- the contract status is changed by an authorized finalization,
- DEC-0009 is accepted,
- M1.2.5 completion criteria are satisfied,
- the delivery PR is merged.

Author self-review, structural validation, a clean Git diff, Draft PR creation, compiler feasibility, or successful future Kernel validation does not constitute human semantic acceptance.

No implementation or merge authorization is granted by this proposal.
