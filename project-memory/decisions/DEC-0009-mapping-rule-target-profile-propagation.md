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
- prerequisite policies,
- selection and precedence policies,
- fallback policies,
- profile and capability constraints,
- governance and effective-time bases.

Any replay-affecting membership, import, or policy change creates a new ruleset revision.

Rule and ruleset identity contains exact capability requirements or predicates, not the identity of the executing compiler build. A changed requirement creates a new rule or ruleset revision; a changed implementation changes the compiler basis.

## Proposed prerequisite model

Every applicable prerequisite receives exactly one disposition:

- `satisfied`,
- `not-satisfied`,
- `unresolved`,
- `not-applicable`.

Omission is not satisfaction or non-applicability. Modeling policy cannot satisfy business-semantic prerequisites.

Every mapping request produces a `MappingEvaluationResult` with complete candidate enumeration, exact filtering, all candidate dispositions or exclusion bases, prerequisite provenance, actual compiler basis, and an exact selection or no-selection result. Omission of a potentially applicable rule makes the evaluation unresolved.

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

Changed rule, ruleset, membership, import, policy, profile, compatibility, transformation, or actual compiler basis is a changed replay basis, not verification of the same replay claim.

The proposal uses only inherited diagnostics and does not change their severity, blocking, aggregation, ordering, or authority rules. `MAPPING_RULESET_UNRESOLVED` is reserved for replay and verification; current compilation closure defects use applicable inherited compilation diagnostics.

## Rationale

Exact references without complete membership and policy closure are insufficient for replay. Deterministic selection without semantic and authority boundaries could silently resolve business ambiguity. Profile names without exact identity or transformation provenance could make compiler and Kernel artifacts disagree about the validation basis.

Complete per-request evaluation provenance prevents unsuccessful evaluations from disappearing. Separating capability requirements from actual compiler identity prevents implementation changes from mutating ruleset identity. Exact compatibility authority prevents agent proposals, Kernel results, or transformation records from becoming unsupported general proof.

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
- ruleset closure exposes hidden imports and policies;
- ruleset requirements remain distinct from the executing compiler basis;
- candidate selection is deterministic without crossing business-authority boundaries;
- target profile remains exact and visible across the pipeline;
- compatibility assessments expose their policy and authority;
- explicit transformations preserve both profile identities and affected scope without becoming semantic proof by themselves.

Costs and constraints:

- more exact provenance must be recorded;
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
- [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20)
- Draft [PR #26](https://github.com/ThresholdOps/MotiveForce/pull/26)

## Follow-up actions

1. Complete author structural and consistency validation of the four REV-0011 corrections.
2. Obtain human semantic and design re-review under REV-0012 through Draft [PR #26](https://github.com/ThresholdOps/MotiveForce/pull/26).
3. Keep DEC-0009 Proposed until an authorized later finalization and merge.
4. Do not start implementation, Issue #8, Issue #9, or Issue #21.

## Decision effect

REV-0011 retains the overall architecture and requests four bounded changes. No acceptance, implementation authorization, ready-for-review transition, or merge authorization is granted.
