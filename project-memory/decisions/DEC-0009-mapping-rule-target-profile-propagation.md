# DEC-0009: Mapping Rule References and Target BPMN Profile Propagation

- Decision ID: `DEC-0009`
- Title: Mapping Rule References and Target BPMN Profile Propagation
- Status: Proposed
- Date: 2026-07-27T12:35:18Z
- Decision authority: Pending human semantic and design review
- Related Issue: [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20)
- Related milestone: [M1.2.5](../milestones/M1-2-5-mapping-rule-target-profile-propagation.md)
- Source branch: `design/m1-2-5-mapping-profile-propagation`
- Draft PR: [PR #26](https://github.com/ThresholdOps/MotiveForce/pull/26)
- Exact base: [`20f53f13938692b9c572b6f9f963e89fc22cb5b8`](https://github.com/ThresholdOps/MotiveForce/commit/20f53f13938692b9c572b6f9f963e89fc22cb5b8)
- Initial source head: [`1e874144aa68e444669a55913d44d1ab0dc73538`](https://github.com/ThresholdOps/MotiveForce/commit/1e874144aa68e444669a55913d44d1ab0dc73538)
- Final source head: Recorded in PR and Issue metadata after the final self-provenance amend
- Human review round 1: [REV-0011](../reviews/M1-2-5-mapping-rule-target-profile-propagation-review.md), Request changes against [`1cb85a81b00bce4729bfc2ce58ad871ab67ee1d0`](https://github.com/ThresholdOps/MotiveForce/commit/1cb85a81b00bce4729bfc2ce58ad871ab67ee1d0)
- Independent re-review: [REV-0012](../reviews/M1-2-5-mapping-rule-target-profile-propagation-review-2.md), Request changes against [`7a6ec176a0fcc738a5c56a9c98a7d946446a2c01`](https://github.com/ThresholdOps/MotiveForce/commit/7a6ec176a0fcc738a5c56a9c98a7d946446a2c01)
- Proposed correction: `REV12-FIND-001` and `REV12-FIND-002` addressed; bounded reviewer-attention clarifications for imported enumeration-policy authority, current candidate-source failure ownership, and replay-policy precedence are included; pending human semantic and design re-review under REV-0013
- Supersedes: None
- Superseded by: None

## Context

Accepted M1 assigns mapping eligibility and mapping application to the Semantic Compiler, requires an exact target profile across compilation and Kernel validation, and separates agent proposals from compiler and Kernel authority. Accepted M1.2.1 requires exact immutable revision and external-authoritative-basis references. Accepted M1.2.2 requires exact mapping-ruleset and target-profile replay bases. Accepted M1.2.3 defines diagnostic policy, and accepted M1.2.4 defines current authority for `AnalystDecision`.

The remaining M1.2 gap is a bounded contract for exact mapping-rule and ruleset identity, prerequisite assessment, deterministic selection, profile compatibility and transformation, propagation, and provenance.

## Proposed decision

Adopt the Proposed [Mapping Rule References and Target BPMN Profile Propagation Contract](../../docs/MAPPING_RULE_TARGET_PROFILE_PROPAGATION_CONTRACT.md) for human review.

The proposal defines:

- logical and immutable revision identity for mapping rules,
- exact `MappingRuleRef`,
- exact closed `MappingRulesetRef`,
- exact immutable `CandidateEnumerationPolicyRef` as a member of ruleset closure,
- pre-evaluation `CandidateUniverseRecord`,
- immutable ruleset membership and imports,
- rule lifecycle and supersession,
- explicit prerequisite categories and dispositions,
- exact `PrerequisiteSatisfactionRecord`,
- complete candidate coverage and one `MappingEvaluationResult` for every request,
- candidate applicability and eligibility dispositions,
- exact `MappingRuleApplication`,
- deterministic selection among semantically equivalent eligible candidates,
- prohibition on precedence or fallback resolving conflicting business meaning,
- bounded non-degrading fallback,
- exact `TargetBPMNProfileRef`,
- exact authorized directional `ProfileCompatibilityAssessment`,
- explicit `ProfileTransformationBasis`,
- profile propagation across compiler, replay, and Kernel artifacts,
- mapping provenance,
- inherited diagnostic behavior,
- Issue #8, Issue #9, and Issue #21 boundaries.

## Proposed rule and ruleset identity

One stable logical rule identity may have multiple immutable revisions. Authoritative use requires one exact revision, not a logical identifier, version range, latest selector, or mutable locator.

One exact ruleset revision closes:

- exact rule membership,
- exact imported rulesets,
- one exact immutable candidate-enumeration policy revision,
- prerequisite policies,
- selection and precedence policies,
- fallback policies,
- profile and capability constraints,
- governance and effective-time bases.

The request-selected top-level ruleset owns the one operative candidate-enumeration relationship for a mapping request. Its directly owned policy enumerates the complete imported closure. Imported rulesets retain their exact policies as immutable transitive identity and replay provenance, but those policies are inert for the importing request and neither override nor supplement the request-selected policy. A policy difference alone is not a conflict; claiming more than one operative policy for the same request is.

Any replay-affecting membership, import, candidate-enumeration policy, or other policy change creates a new ruleset revision. Changing an imported policy creates a new imported ruleset revision and therefore a new importing ruleset revision when that import is selected. A changed candidate-enumeration policy changes the semantic evaluation and replay basis even when candidate identities and output remain identical.

Rule and ruleset identity contains exact capability requirements or predicates, not the identity of the executing compiler build. A changed requirement creates a new rule or ruleset revision; a changed implementation changes the compiler basis.

## Proposed prerequisite model

Every applicable prerequisite receives exactly one disposition:

- `satisfied`,
- `not-satisfied`,
- `unresolved`,
- `not-applicable`.

Omission is not satisfaction or non-applicability. Modeling policy cannot satisfy business-semantic prerequisites.

Every mapping request first produces a `CandidateUniverseRecord` under the ruleset-owned exact candidate-enumeration policy and then produces a `MappingEvaluationResult`. The universe record identifies consulted sources, complete expected candidate identities, pre-evaluation exclusions, unavailable or non-evaluable candidates, deduplication or equivalence decisions, ordering basis, provenance, and diagnostics.

Every expected candidate receives exactly one candidate disposition or exact pre-evaluation exclusion basis. `MappingEvaluationResult` references exactly one universe record and policy revision. Omission of an expected candidate emits `PROVENANCE_MISSING`, makes the request unresolved, and cannot be interpreted as exclusion, inapplicability, or ineligibility.

Current candidate-source failures are phase-owned: a mutable selector uses `FLOATING_EXTERNAL_BASIS`; an exact required source reference that cannot resolve uses `UNRESOLVED_REFERENCE`; an otherwise valid and evaluable source blocked only by unrealized compiler capability uses `UNSUPPORTED_MAPPING`; and, after the exact source reference resolves, a completed deterministic assessment that cannot establish required authoritative candidate-universe provenance uses `PROVENANCE_MISSING`. A runtime or infrastructure failure that prevents the assessment from completing remains an execution failure and emits no semantic mapping diagnostic for that interrupted assessment.

## Proposed mapping application and selection

`MappingRuleApplication` is compiler-owned provenance for applying one exact selected rule to exact semantic inputs under exact ruleset, evaluation, prerequisite, selection, policy, profile, authority, and compiler bases. It references the `MappingEvaluationResult` and exists only when the rule was actually applied.

Selection:

- occurs only among eligible semantically equivalent candidates,
- requires an exact accepted selection basis,
- is independent of incidental runtime ordering,
- cannot resolve conflicting business meaning,
- cannot override prerequisites,
- cannot silently degrade unsupported meaning through generic fallback.

## Proposed target-profile policy

`TargetBPMNProfileRef` identifies one exact immutable target profile. Names, mutable URLs, latest selectors, and version labels that can denote multiple contents are insufficient.

`ProfileCompatibilityAssessment` is directional, exact, scoped, version-specific, and based on exact policy, evaluator, authority, provenance, time, and diagnostics, with conceptual outcomes `compatible`, `incompatible`, or `unresolved`. Agent proposals remain non-authoritative, compiler derivation requires a fully applicable Accepted deterministic policy, and model-specific Kernel validation is not general profile compatibility.

Profile substitution requires an exact `ProfileTransformationBasis`, preserves source and target identities, produces a new result, and remains replay-affecting. The basis alone does not prove semantic preservation; a semantic-changing transformation requires a new mapping evaluation, application, compiled model, and compilation result.

## Proposed propagation and provenance

The same exact profile propagates through:

- `CompilationPolicyContext`,
- compilation request,
- `ProposedBPMNMapping` where applicable,
- `MappingRuleApplication`,
- `CompiledSemanticModel`,
- `CompilationResult`,
- `CompilationReplayManifest`,
- `KernelValidationReport`.

Compiler outputs must retain exact semantic inputs, current-authority bases, rule, ruleset, prerequisite, selection, profile, policy, transformation, and compiled-element provenance.

## Replay and diagnostics

Changed rule, ruleset, membership, import, candidate-enumeration policy, other policy, profile, compatibility, transformation, or actual compiler basis is a changed replay basis, not verification of the same replay claim.

The proposal uses only inherited diagnostics and does not change their severity, blocking, aggregation, ordering, or authority rules. Its normative trigger and precedence matrix assigns:

- `UNRESOLVED_REFERENCE` to unresolvable, malformed, cyclic, or impossible current reference closure;
- `PROVENANCE_MISSING` to current candidate-coverage omission;
- `UNSUPPORTED_MAPPING` to an otherwise valid mapping whose required capability is not realized by the actual compiler;
- `MAPPING_NOT_ELIGIBLE` to non-capability candidate eligibility failure when no more specific inherited diagnostic applies;
- `MODELING_POLICY_REQUIRED` to missing or contradictory governing modeling policy;
- `MAPPING_RULESET_UNRESOLVED` only to replay or verification inability to reconstruct exact historical ruleset closure.

Historical input absence, exact dependency unavailability, missing or floating policy, and available but changed exact basis retain their distinct inherited replay diagnostics.

For replay, `REPLAY_POLICY_UNRESOLVED` is the sole primary code for an absent policy identity or incomplete frozen policy parameters. `REPLAY_INPUT_CLOSURE_INCOMPLETE` is limited to absent non-policy inputs and candidate-universe evidence after the exact applicable policy identity and parameters are present. The same missing policy basis does not emit both codes.

## Rationale

Exact references without complete membership and policy closure are insufficient for replay. Deterministic selection without semantic and authority boundaries could silently resolve business ambiguity. Profile names without exact identity or transformation provenance could make compiler and Kernel artifacts disagree about the validation basis.

An immutable request-selected-ruleset-owned candidate-enumeration policy and pre-evaluation universe record prevent a compiler from changing the candidate population while claiming the same ruleset basis. Explicit imported-policy inertness prevents one import graph from acquiring multiple operative enumeration policies. Complete per-request evaluation provenance prevents unsuccessful evaluations from disappearing. Deterministic phase-owned diagnostics, including candidate-source and replay-policy precedence, prevent the same failure from acquiring different replay-semantic codes. Separating capability requirements from actual compiler identity prevents implementation changes from mutating ruleset identity. Exact compatibility authority prevents agent proposals, Kernel results, or transformation records from becoming unsupported general proof.

The proposal closes those gaps while preserving accepted authority domains and deferring implementation.

## Alternatives considered

### Rule version labels only

Rejected for the proposal because one label may identify multiple contents and cannot guarantee immutable replay identity.

### Mutable latest ruleset

Rejected because membership and policy could change between compilation and replay.

### Storage-order or priority-only selection

Rejected because incidental ordering is not a semantic policy and priority must not resolve business ambiguity or failed prerequisites.

### Generic fallback for unsupported meaning

Rejected because it can hide lost or invented business semantics.

### Profile name or family as exact identity

Rejected because family labels and names do not freeze profile content or compatibility.

### Symmetric compatibility

Rejected because compatibility can be directional and scope-specific.

### Silent compatible profile substitution

Rejected because even compatible exact profiles are distinct provenance and replay bases.

### Kernel-owned mapping selection

Rejected because the accepted authority chain assigns mapping eligibility and application to the Semantic Compiler.

### Agent-authored authoritative mapping application

Rejected because `ProposedBPMNMapping` remains non-authoritative.

### Implement a profile registry or metamodel now

Rejected as out of scope and retained by Issue #9 and later implementation work.

## Consequences

Positive:

- mapping decisions become exactly traceable and replayable;
- unsuccessful, blocked, unresolved, and no-selection evaluations retain complete candidate provenance;
- candidate coverage is verified against one immutable pre-evaluation universe;
- ruleset closure exposes hidden imports and policies;
- ruleset requirements remain distinct from the executing compiler basis;
- candidate selection is deterministic without crossing business-authority boundaries;
- current compilation, replay reconstruction, and changed-basis diagnostics remain phase-distinct;
- target profile remains exact and visible across the pipeline;
- compatibility assessments expose their policy and authority;
- explicit transformations preserve both profile identities and affected scope without becoming semantic proof by themselves.

Costs and constraints:

- more exact provenance must be recorded;
- every ruleset revision must close one exact candidate-enumeration policy revision;
- every mapping request requires a complete evaluation result even when no rule is applied;
- ruleset and profile changes require new immutable revisions;
- incomplete prerequisite or compatibility bases block authoritative scope;
- profile transformation produces a new artifact rather than mutating an existing one;
- human semantic review is required before acceptance.

## Dependencies and boundaries

- Accepted M1 through M1.2.4 contracts and DEC-0005 through DEC-0008.
- Issue #8 retains detailed partial-compilation dependency closure.
- Issue #9 retains BPMN metamodel-generation and conformance strategy.
- Issue #21 retains executable contract-test matrix work.
- No Issue is started except Issue #20 design work.

## Related artifacts

- [M1.2.5 contract](../../docs/MAPPING_RULE_TARGET_PROFILE_PROPAGATION_CONTRACT.md)
- [M1.2.5 milestone](../milestones/M1-2-5-mapping-rule-target-profile-propagation.md)
- [M1.2 parent milestone](../milestones/M1-2-process-ir-machine-readiness.md)
- [REV-0011](../reviews/M1-2-5-mapping-rule-target-profile-propagation-review.md)
- [REV-0012](../reviews/M1-2-5-mapping-rule-target-profile-propagation-review-2.md)
- [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20)
- Draft [PR #26](https://github.com/ThresholdOps/MotiveForce/pull/26)

## Follow-up actions

1. Complete author structural and consistency validation of the Proposed corrections for `REV12-FIND-001`, `REV12-FIND-002`, and the three bounded reviewer-attention clarifications.
2. Obtain human semantic and design re-review under REV-0013 through Draft [PR #26](https://github.com/ThresholdOps/MotiveForce/pull/26).
3. Keep DEC-0009 Proposed until an authorized later finalization and merge.
4. Do not start implementation, Issue #8, Issue #9, or Issue #21.

## Decision effect

REV-0012 retains the overall architecture and requests two bounded changes. This Proposed correction addresses them and records three bounded reviewer-attention clarifications for REV-0013 re-review, but does not close any item by review. No acceptance, implementation authorization, ready-for-review transition, or merge authorization is granted.
