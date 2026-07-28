# REV-0012: M1.2.5 Mapping Rule and Target Profile Propagation Re-Review

- Review ID: `REV-0012`
- Review date: 2026-07-28T09:10:51Z
- Reviewer role: Independent AI semantic and architectural reviewer preparing evidence for separate human acceptance
- Repository: [ThresholdOps/MotiveForce](https://github.com/ThresholdOps/MotiveForce)
- Reviewed artifact: [docs/MAPPING_RULE_TARGET_PROFILE_PROPAGATION_CONTRACT.md](../../docs/MAPPING_RULE_TARGET_PROFILE_PROPAGATION_CONTRACT.md)
- Reviewed commit: [`7a6ec176a0fcc738a5c56a9c98a7d946446a2c01`](https://github.com/ThresholdOps/MotiveForce/commit/7a6ec176a0fcc738a5c56a9c98a7d946446a2c01)
- Base commit: [`20f53f13938692b9c572b6f9f963e89fc22cb5b8`](https://github.com/ThresholdOps/MotiveForce/commit/20f53f13938692b9c572b6f9f963e89fc22cb5b8)
- Branch: `design/m1-2-5-mapping-profile-propagation`
- Related PR: Draft [PR #26](https://github.com/ThresholdOps/MotiveForce/pull/26)
- Related Issue: [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20)
- Previous review: [REV-0011](M1-2-5-mapping-rule-target-profile-propagation-review.md)
- Review type: Independent semantic and architectural re-review
- Review status: Completed
- Review outcome: Request changes
- Decision effect: Evidence for human consideration only; no acceptance and no merge authorization
- Implementation effect: None; implementation remains not started

## 1. Review authority and boundary

This review independently evaluates the Proposed M1.2.5 design at exact commit `7a6ec176a0fcc738a5c56a9c98a7d946446a2c01`.

It does not claim that human review or human acceptance occurred. It does not accept the contract or DEC-0009, complete M1.2.5, authorize implementation or merge, change PR #26 from Draft, or close Issue #20.

The review covers the complete M1.2.5 contract and concentrates on the four REV-0011 corrections. It excludes machine representation, runtime implementation, compiler or Kernel code, profile registries, generated metamodels, executable validation, tests, CI, APIs, persistence, and Issue #8 dependency-closure implementation.

## 2. Evidence inspected

- Proposed [M1.2.5 contract](../../docs/MAPPING_RULE_TARGET_PROFILE_PROPAGATION_CONTRACT.md) and [DEC-0009](../decisions/DEC-0009-mapping-rule-target-profile-propagation.md).
- [REV-0011](M1-2-5-mapping-rule-target-profile-propagation-review.md) and the exact correction diff from `1cb85a81b00bce4729bfc2ce58ad871ab67ee1d0` to the reviewed commit.
- Accepted [M1 Process IR contract](../../docs/PROCESS_IR_CONTRACT.md).
- Accepted [M1.2.1 RecordEnvelope contract](../../docs/PROCESS_IR_RECORD_ENVELOPE_CONTRACT.md).
- Accepted [M1.2.2 replay contract](../../docs/SEMANTIC_COMPILER_REPLAY_CONTRACT.md).
- Accepted [M1.2.3 diagnostic policy](../../docs/PROCESS_IR_DIAGNOSTIC_POLICY_CONTRACT.md).
- Accepted [M1.2.4 AnalystDecision staleness contract](../../docs/ANALYST_DECISION_STALENESS_REVALIDATION_CONTRACT.md).
- Accepted DEC-0005 through DEC-0008.
- Project-memory review template, review index, governance conventions, M1.2.5 milestone, parent M1.2 milestone, and open-item state.
- GitHub PR #26, Issue #20, and deferred Issues #6, #8, #9, and #21.

## 3. Evidence matrix

| Concept or invariant | Authoritative artifact and producer -> consumer | Immutable identity and provenance | Current, replay, verification, and diagnostic behavior | Assessment and evidence |
| --- | --- | --- | --- | --- |
| Logical rule and revision identity | Rule governance -> Semantic Compiler | Stable logical identity plus exact immutable `MappingRuleRef`; supersession preserves predecessors | Current use forbids floating selection; replay retains old revision | Satisfied by sections 7.1-7.3. |
| Exact ruleset closure | Ruleset governance -> mapping evaluation | Exact membership, imports, policies, capability requirements, and governance basis | Closure must terminate and be reconstructable; current and replay defects use separate diagnostics | Partially satisfied. Sections 8 and 10 require an exact candidate-enumeration/filter policy, but section 8 does not close that policy and section 20 does not explicitly classify its change as a changed replay basis. |
| Prerequisite assessment | Semantic Compiler -> mapping evaluation and application | Exact prerequisite revision, request, semantic inputs, authority, policy, profile, compiler realization, disposition, and basis | Four dispositions; omission is unresolved; policy cannot satisfy business defects | Satisfied by sections 9.1-9.4. |
| Candidate coverage | Semantic Compiler -> `MappingEvaluationResult` | Complete closure, exact enumeration/filter policy, dispositions or exclusion bases | Missing candidate or provenance makes the evaluation unresolved | Current-evaluation boundary is explicit in sections 10.1-10.3; replay closure of the enumeration/filter policy remains incomplete. |
| Mapping application | Semantic Compiler -> compiled model and result | Exact evaluation, rule, ruleset, prerequisites, candidates, policy, profile, compiler, output identity | Exists only when a rule is actually applied; changed basis creates a new application | Satisfied by section 12. |
| Multi-rule selection | Semantic Compiler under accepted policy -> mapping application | Complete eligible set, equivalence basis, selection, precedence, fallback, and tie policy | Equivalent candidates require exact policy; conflicting meaning cannot be selected by priority | Satisfied by section 11. |
| Exact target profile | Compilation policy/request -> compiler -> Kernel | Stable logical profile plus exact immutable revision and exact external basis | No defaults or silent substitution; profile is a replay-affecting basis | Satisfied by sections 13 and 16 and the accepted M1 profile rule. |
| Compatibility authority | Accepted deterministic policy or non-authoritative Agent proposal -> compiler | Exact source/target profiles, direction, scope, policy, evaluator, authority, time, provenance, diagnostics | Three outcomes; Kernel model validation cannot become general compatibility proof | Satisfied by section 14. |
| Profile transformation | Compiler mapping evaluation -> new model/result -> Kernel | Exact source/target profiles, assessment, rules, changed/excluded/unresolved scope, and provenance | Semantic change requires a new evaluation, applications, model, and result; old artifacts remain immutable | Satisfied by section 15. |
| Replay and verification | Compiler/replay manifest -> comparison authority | Exact ruleset, profile, policies, evaluation, applications, compiler identity, and realization | Changed bases are not same replay; historical closure failure is `MAPPING_RULESET_UNRESOLVED` | Partially satisfied by section 20 because candidate-enumeration/filter policy is recorded in an output but not unambiguously closed as a replay input. |
| Partial compilation and Kernel boundary | Compiler -> authoritative fragment -> Kernel | Exact scope registers, dependency closure, model, profile, and provenance | Blocking or unresolved mapping cannot enter an authoritative fragment; Kernel validates but cannot repair or remap | Satisfied at the M1.2.5 boundary by sections 18 and 22.2; detailed closure remains Issue #8. |
| Diagnostic authority | Accepted diagnostic policy -> compiler/replay/Kernel emitters | Exact code and semantic diagnostic projection under exact policy | Current compilation and replay diagnostics must be phase-specific | Partially satisfied. Replay-only reservation is explicit, but current capability and closure cases are not partitioned deterministically. |

## 4. REV-0011 correction verification

### REV11-FIND-001 - Partially resolved

Resolved portions:

- section 10.3 requires one `MappingEvaluationResult` for every request, including refused, blocked, unresolved, and no-selection outcomes;
- sections 10.1-10.3 require complete candidate coverage, exact exclusion bases, omission-as-unresolved behavior, and retained unsuccessful-evaluation provenance;
- section 12 creates `MappingRuleApplication` only when a rule is actually applied.

Remaining defect:

- the exact candidate-enumeration/filter-policy revision required by sections 10.1 and 10.3 is absent from the minimum `MappingRulesetRef` closure in section 8, from ruleset revision triggers in section 8.3, and from the explicit changed-replay-basis list in section 20.

This leaves `REV12-FIND-001`.

### REV11-FIND-002 - Resolved

Sections 8.3, 9.3, 10.3, 12, and 20 separate exact capability requirements or predicates from the executing compiler identity and actual capability realization. Requirement changes revise the rule or ruleset. Compiler implementation or realization changes alter the compiler basis.

### REV11-FIND-003 - Resolved

Section 14 defines exact compatibility identity, direction, scope, policy, evaluator, authority, provenance, time, diagnostics, and three outcomes. Agent assessments remain non-authoritative, compiler authority requires a fully applicable Accepted deterministic policy, and Kernel validation remains model-specific.

Section 15 states that `ProfileTransformationBasis` alone cannot prove semantic preservation and requires fresh evaluation, application, model, and result provenance for semantic-changing transformation.

### REV11-FIND-004 - Partially resolved

Resolved portion:

- sections 8.2 and 21 and example 22 reserve `MAPPING_RULESET_UNRESOLVED` for replay or verification inability to reconstruct exact historical closure.

Remaining defect:

- the current-compilation diagnostic partition is not determinate for all owned closure and capability defects. Sections 10.2 and 21 overlap `UNSUPPORTED_MAPPING` and `MAPPING_NOT_ELIGIBLE` for an unrealized capability prerequisite. Section 8.2 lists possible diagnostics but does not assign cyclic or policy-conflicting current closure to an exact inherited code. Candidate-coverage omission is unresolved but has no exact current diagnostic assignment.

This leaves `REV12-FIND-002`.

## 5. Required review questions

| ID | Answer | Basis |
| --- | --- | --- |
| `RQ-01` | No, not fully. | Logical and revision identity are separated, but exact ruleset/replay closure does not unambiguously include the candidate-enumeration/filter-policy revision. |
| `RQ-02` | Yes. | Sections 9 and 10 define exact prerequisites, four dispositions, authority, supporting basis, omission behavior, and compiler realization evidence. |
| `RQ-03` | Yes. | Sections 10, 12, and 18 separate Agent proposals, rule and ruleset definitions, compiler evaluation, actual application, and Kernel validation. |
| `RQ-04` | Yes. | Section 11 permits deterministic selection only among eligible semantically equivalent candidates and forbids precedence or fallback from resolving conflicting meaning or failed prerequisites. |
| `RQ-05` | Yes. | Sections 13-15 define exact profile identity, directional scoped compatibility, authority, and non-mutating explicit transformation with fresh provenance. |
| `RQ-06` | Yes. | Sections 10, 12, 16, 17, and 20 propagate exact profile identity through requests, evaluation, compiler outputs, replay, comparison bases inherited from M1.2.2, and Kernel-facing artifacts. |
| `RQ-07` | No, not fully. | Authority and Issue boundaries are clean, but current diagnostic selection is ambiguous for capability mismatch, candidate omission, and some ruleset-closure failures. |
| `RQ-08` | No. | Two blocking determinism findings remain, so the design is not ready for human acceptance consideration. |

## 6. End-to-end scenario results

| Scenario | Determinism and outcome | Authoritative artifact and required provenance | Failure diagnostic | Kernel and replay result |
| --- | --- | --- | --- | --- |
| `SCN-01` Successful exact-profile mapping | Deterministic when all prerequisites are satisfied | `MappingEvaluationResult`, actual `MappingRuleApplication`, model, and result with exact rule, ruleset, profile, compiler, inputs, and outputs | None on success | Kernel validates exact model/profile; replay can reproduce exact basis. |
| `SCN-02` Compatible equivalent representation | Deterministic under exact accepted equivalence and selection policy; otherwise blocked | Exact evaluation, equivalence basis, compatibility assessment where applicable, selected and non-selected rules | `EQUIVALENT_BPMN_REPRESENTATIONS` when selection policy is absent | Kernel validates selected result only; replay captures policy and profile. |
| `SCN-03` Semantic-changing transformation | Deterministic only through a fresh mapping and compilation outcome | New evaluation, applications, model, result, exact profiles, transformation rules, assessment, and changed scope | `PROVENANCE_MISSING`, `TARGET_BPMN_PROFILE_MISMATCH`, or applicable prerequisite diagnostic when required basis is absent | Kernel receives only new exact model; replay treats transformation change as changed basis. |
| `SCN-04` Multiple applicable rules | Equivalent rules are selected by exact policy or explicitly blocked; conflicting meaning remains unresolved | Complete candidate set, equivalence basis, selection/precedence policy, and all dispositions | `EQUIVALENT_BPMN_REPRESENTATIONS` or applicable inherited business-semantic diagnostic | No unresolved mapping enters Kernel; replay reproduces exact selection basis. |
| `SCN-05` Explicitly excluded candidate | Deterministic | Exact rule, request, scope, filter policy, exclusion condition, and supporting basis | None solely for a valid exclusion | Kernel sees only resulting authoritative model; replay can reproduce exclusion if policy is frozen. |
| `SCN-06` Omitted candidate | Current semantic outcome is explicitly unresolved, but replay input identity is incomplete | `MappingEvaluationResult` must retain the coverage gap and known provenance | Exact current diagnostic is not assigned | Unresolved scope cannot enter Kernel; replay may be unstable if the filter-policy basis is not closed. |
| `SCN-07` Current compilation closure failure | Unresolved import is deterministic; cyclic and policy-conflicting closure diagnostics are underdetermined | Current evaluation with exact attempted ruleset closure and defect provenance | `UNRESOLVED_REFERENCE` for unavailable import; exact code for cycle/conflict is not specified | Affected scope cannot enter Kernel; historical replay remains a separate operation. |
| `SCN-08` Historical replay success | Deterministic with exact historical closure | Manifest, exact rule/ruleset/profile/policies/compiler and evaluation/application provenance | None on exact match | Kernel validation is not required to prove replay comparison; replay reproduces original semantics. |
| `SCN-09` Historical replay failure | Deterministic | Manifest and exact record of missing historical closure basis | `MAPPING_RULESET_UNRESOLVED`; result `not replayable` | No claim of Kernel or current validity; verification reports unreconstructable closure. |
| `SCN-10` Partial compilation | Deterministic at the defined boundary; detailed dependency algorithm remains Issue #8 | Scope registers, fragment closure, evaluations, applications, diagnostics, exact profile | Applicable scope-local inherited diagnostic | Kernel receives only authoritative fragments; unresolved mapping remains visible; replay captures partial basis. |
| `SCN-11` Compiler capability mismatch | Blocking outcome is deterministic, diagnostic code is not | Capability requirement, actual compiler identity and realization, prerequisite record, evaluation | Both `UNSUPPORTED_MAPPING` and `MAPPING_NOT_ELIGIBLE` match current wording | Blocked scope cannot enter Kernel; replay captures compiler basis but same-policy diagnostic projection can drift. |
| `SCN-12` Profile directionality | Deterministic under exact assessment; reverse direction is separately assessed | Exact source/target profiles, direction, scope, policy, evaluator, authority, time, and diagnostics | `TARGET_BPMN_PROFILE_MISMATCH` only for exact incompatibility; unresolved basis remains unresolved | Kernel validation remains model-specific; replay captures exact directional basis. |

## 7. Diagnostic-boundary assessment

The 16 inherited diagnostic codes retain exact spelling. No code is added, removed, renamed, merged, reclassified, or assigned a new severity.

The following boundaries are clear:

- missing profile uses `TARGET_BPMN_PROFILE_REQUIRED`;
- incompatible pipeline profiles use `TARGET_BPMN_PROFILE_MISMATCH`;
- historical ruleset closure reconstruction failure uses `MAPPING_RULESET_UNRESOLVED`;
- floating historical dependency uses `FLOATING_REPLAY_DEPENDENCY`;
- available but changed exact replay basis uses `REPLAY_NOT_COMPARABLE`;
- missing exact current reference uses `UNRESOLVED_REFERENCE`.

The following current-compilation boundaries remain ambiguous:

- unrealized compiler capability can satisfy both `UNSUPPORTED_MAPPING` and `MAPPING_NOT_ELIGIBLE`;
- omitted candidate coverage becomes unresolved without an exact assigned current diagnostic;
- cyclic and policy-conflicting active ruleset closure have no exact inherited diagnostic assignment.

Because diagnostic code is part of the accepted semantic diagnostic projection, this ambiguity can produce replay-visible diagnostic drift under otherwise identical bases.

## 8. Contract and decision compatibility

Accepted contracts and DEC-0005 through DEC-0008 are unchanged at the reviewed commit.

The corrected design preserves:

- M1 Agent, compiler, and Kernel authority boundaries;
- M1.2.1 exact-reference and immutability rules;
- M1.2.2 changed-basis and replay-comparison boundaries;
- M1.2.3 severity, blocking, and semantic diagnostic projection;
- M1.2.4 current-authority rules.

DEC-0009 remains Proposed and accurately summarizes the corrected architecture, but it inherits the two unresolved contract gaps. No implementation commitment, schema, algorithm, registry, compiler, Kernel, API, persistence, test, or CI artifact is introduced.

## 9. Findings

### REV12-FIND-001 - Candidate-enumeration policy is not closed as an exact replay input

- Severity: Blocking
- Affected concept: `MappingRulesetRef`, candidate coverage, and deterministic replay closure
- Evidence: `docs/MAPPING_RULE_TARGET_PROFILE_PROPAGATION_CONTRACT.md`, sections 8, 10.1, 10.3, and 20
- Violated invariants: exact ruleset closure; complete candidate coverage; replay stability
- Failure scenario: The same exact ruleset revision is evaluated under exact filter policy `F1`, which includes rule `R`, and `F2`, which excludes it. Sections 10.1 and 10.3 record the policy in the result, but sections 8 and 20 do not unambiguously freeze it as a ruleset or separate replay input or classify its change as a changed replay basis.
- Why insufficient: Recording a policy in evaluation provenance after execution does not define where the replay-affecting policy is authoritatively closed before execution. Two executions can declare the same ruleset identity while enumerating different candidate sets.
- Required correction: Place the exact candidate-enumeration/filter-policy reference in the authoritative ruleset closure or in another explicitly named exact request/policy basis; propagate it into `CompilationReplayManifest`; state whether a change creates a new ruleset revision or another changed replay basis; require every closure member to be accounted for by disposition or exact exclusion under that policy.
- Acceptance test: With all other bases identical, changing `F1` to `F2` must be identified before semantic comparison as a changed exact basis and produce `not comparable`, while a missing or floating filter policy must make current evaluation unresolved and replay not replayable under an exact inherited diagnostic.

### REV12-FIND-002 - Current diagnostic selection is not a non-overlapping deterministic partition

- Severity: Blocking
- Affected concept: current mapping/ruleset closure and compiler-capability diagnostics
- Evidence: `docs/MAPPING_RULE_TARGET_PROFILE_PROPAGATION_CONTRACT.md`, sections 8.2, 10.2, and 21
- Violated invariants: deterministic current diagnostic ownership; unchanged diagnostic meaning; replay-stable semantic diagnostic projection
- Failure scenario: A rule requires capability `C`, but the exact compiler does not realize `C`. Section 10.2 and the `UNSUPPORTED_MAPPING` row select `UNSUPPORTED_MAPPING`, while the `MAPPING_NOT_ELIGIBLE` row also covers failed capability prerequisites. Separately, cyclic or policy-conflicting current ruleset closure and candidate-coverage omission have no exact diagnostic assignment.
- Why insufficient: Two conforming implementations can emit different diagnostic codes for the same exact condition. Since diagnostic code participates in semantic replay comparison, the same basis can produce an artificial semantic mismatch.
- Required correction: Define a non-overlapping decision table for current closure, candidate-coverage, and capability-realization failures using only inherited codes. Specify the exact primary code or exact permitted code set for unresolved imports, floating bases, cycles, policy conflicts, omitted candidate coverage, unsupported requested behavior, and failed candidate capability prerequisites. Keep `MAPPING_RULESET_UNRESOLVED` replay-only.
- Acceptance test: `SCN-06`, `SCN-07`, and `SCN-11` each yield one exact prescribed diagnostic projection under the same policy; historical closure reconstruction failure alone yields `MAPPING_RULESET_UNRESOLVED`; a changed exact basis yields `REPLAY_NOT_COMPARABLE`.

## 10. Review outcome

`Request changes`

REV11-FIND-002 and REV11-FIND-003 are resolved. REV11-FIND-001 and REV11-FIND-004 are only partially resolved because `REV12-FIND-001` and `REV12-FIND-002` remain.

The architecture remains coherent and is retained. The remaining corrections are bounded to exact policy closure and deterministic diagnostic partitioning. No new subsystem, diagnostic code, implementation, or architecture redesign is required.

The Proposed design is not yet ready for separate human acceptance consideration.

## 11. Explicit status

| Status | Value |
| --- | --- |
| REV-0012 completed | Yes |
| REV-0012 outcome | Request changes |
| Human acceptance performed | No |
| PR #26 merged | No |
| PR #26 Draft | Yes |
| Mapping/profile policy accepted | No |
| DEC-0009 accepted | No |
| M1.2.5 completed | No |
| Issue #20 closed | No |

## 12. Provenance qualification

The complete Proposed M1.2.5 contract at `7a6ec176a0fcc738a5c56a9c98a7d946446a2c01` was reviewed against the listed repository evidence and scenarios. This record is an independent AI-prepared review and evidence package. It is not human semantic acceptance.
