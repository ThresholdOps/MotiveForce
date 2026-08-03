# M1.2.5: Mapping Rule References, Ruleset Versioning, and Target BPMN Profile Propagation

- Milestone ID: `M1.2.5`
- Title: Mapping Rule References, Ruleset Versioning, and Target BPMN Profile Propagation Policy
- Decision status: Accepted through merge of PR #26
- Milestone status: Completed as design-contract work through merge of PR #26
- Implementation status: Design contract completed through merge; runtime implementation not started
- Tracking Issue: [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20)
- Active branch: `design/m1-2-5-mapping-profile-propagation`
- Delivery PR: [PR #26](https://github.com/ThresholdOps/MotiveForce/pull/26), squash-merged as [`2387307f2f7a3f05b65197497b9f0945bb26bf6a`](https://github.com/ThresholdOps/MotiveForce/commit/2387307f2f7a3f05b65197497b9f0945bb26bf6a)
- Exact base: [`20f53f13938692b9c572b6f9f963e89fc22cb5b8`](https://github.com/ThresholdOps/MotiveForce/commit/20f53f13938692b9c572b6f9f963e89fc22cb5b8)
- Human semantic and design review round 1: [REV-0011](../reviews/M1-2-5-mapping-rule-target-profile-propagation-review.md), completed with Request changes against [`1cb85a81b00bce4729bfc2ce58ad871ab67ee1d0`](https://github.com/ThresholdOps/MotiveForce/commit/1cb85a81b00bce4729bfc2ce58ad871ab67ee1d0)
- Independent semantic and architectural re-review: [REV-0012](../reviews/M1-2-5-mapping-rule-target-profile-propagation-review-2.md), completed with Request changes against [`7a6ec176a0fcc738a5c56a9c98a7d946446a2c01`](https://github.com/ThresholdOps/MotiveForce/commit/7a6ec176a0fcc738a5c56a9c98a7d946446a2c01)
- Final human semantic and design review: [REV-0013](../reviews/M1-2-5-mapping-rule-target-profile-propagation-review-3.md), Approve against frozen semantic head [`f8d2249e4693305b57bf021c76bdd78b010da24b`](https://github.com/ThresholdOps/MotiveForce/commit/f8d2249e4693305b57bf021c76bdd78b010da24b); both REV-0012 findings closed and all three section 26.1 clarifications approved

## Objective

Define an Accepted semantic and machine-readiness contract for exact, immutable, replayable, deterministic, profile-scoped Semantic Compiler mapping decisions.

## Scope

- logical mapping-rule identity,
- immutable mapping-rule revisions,
- exact `MappingRuleRef`,
- exact closed `MappingRulesetRef`,
- one exact request-selected-ruleset-owned candidate-enumeration policy across the imported closure, inert imported-policy provenance, and an authoritative pre-evaluation candidate universe,
- ruleset membership, imports, lifecycle, and supersession,
- prerequisite definitions and satisfaction records,
- complete candidate coverage and per-request `MappingEvaluationResult`,
- mapping-rule applicability and candidate dispositions,
- deterministic selection, precedence, equivalent candidates, and bounded fallback,
- `MappingRuleApplication` provenance,
- exact `TargetBPMNProfileRef`,
- directional and scoped profile compatibility,
- exact compatibility-assessment authority,
- explicit profile transformation,
- profile propagation through compiler, replay, and Kernel artifacts,
- M1.2.4 current-authority interaction,
- inherited diagnostic crosswalk,
- Issue #8, Issue #9, and Issue #21 boundaries,
- synthetic examples and manual review tests.

## Explicit non-goals

- No mapping-rule source code.
- No rules engine.
- No Semantic Compiler implementation.
- No BPMN Kernel implementation.
- No profile registry.
- No generated BPMN metamodel.
- No copied protected specification material.
- No schema, parser, validator, or executable compatibility checker.
- No runtime logging, API, persistence, or UI.
- No tests, fixtures, or CI.
- No identifier, hash, or canonical serialization selection.

## Deliverables

- Accepted [mapping and target-profile contract](../../docs/MAPPING_RULE_TARGET_PROFILE_PROPAGATION_CONTRACT.md).
- Accepted [DEC-0009](../decisions/DEC-0009-mapping-rule-target-profile-propagation.md).
- This milestone record.
- M1.2 parent and materially affected project-memory synchronization.
- Updated Issue #20 and PR #26 metadata.

## Accepted dependencies

- [M1 Process IR contract](../../docs/PROCESS_IR_CONTRACT.md).
- [M1.2.1 RecordEnvelope contract](../../docs/PROCESS_IR_RECORD_ENVELOPE_CONTRACT.md).
- [M1.2.2 replay contract](../../docs/SEMANTIC_COMPILER_REPLAY_CONTRACT.md).
- [M1.2.3 diagnostic policy](../../docs/PROCESS_IR_DIAGNOSTIC_POLICY_CONTRACT.md).
- [M1.2.4 staleness and revalidation contract](../../docs/ANALYST_DECISION_STALENESS_REVALIDATION_CONTRACT.md).
- DEC-0005 through DEC-0008.
- M1.2.1 through M1.2.4 Accepted / Completed status.

## Acceptance criteria

- [x] Human semantic and design review is completed.
- [x] Rule logical identity and immutable revision model are accepted.
- [x] Exact ruleset identity, membership, imports, and closure are accepted.
- [x] Prerequisite categories, dispositions, and satisfaction semantics are accepted.
- [x] `MappingRuleApplication` and complete mapping provenance are accepted.
- [x] Deterministic applicability, selection, precedence, equivalence, and fallback boundaries are accepted.
- [x] Exact target-profile identity is accepted.
- [x] Directional compatibility and explicit transformation semantics are accepted.
- [x] Profile propagation across compiler, replay, and Kernel artifacts is accepted.
- [x] Diagnostic and deferred-Issue boundaries are accepted.
- [x] Contract status changes to Accepted through authorized finalization.
- [x] DEC-0009 changes to Accepted through authorized finalization.
- [x] Delivery PR is merged.
- [x] Project memory is synchronized with the approved through-merge transition.

All design-contract and finalization criteria are complete. The final repository transition and Issue closure remain conditioned on merge of PR #26.

## Related PR

[PR #26](https://github.com/ThresholdOps/MotiveForce/pull/26) was opened from initial source head [`1e874144aa68e444669a55913d44d1ab0dc73538`](https://github.com/ThresholdOps/MotiveForce/commit/1e874144aa68e444669a55913d44d1ab0dc73538). REV-0013 reviewed semantic head [`f8d2249e4693305b57bf021c76bdd78b010da24b`](https://github.com/ThresholdOps/MotiveForce/commit/f8d2249e4693305b57bf021c76bdd78b010da24b). The bounded-finalization source head is [`04d1db644bab4ab0e30973cda57a57d6065ec019`](https://github.com/ThresholdOps/MotiveForce/commit/04d1db644bab4ab0e30973cda57a57d6065ec019), and the squash merge on `main` is [`2387307f2f7a3f05b65197497b9f0945bb26bf6a`](https://github.com/ThresholdOps/MotiveForce/commit/2387307f2f7a3f05b65197497b9f0945bb26bf6a).

## Human review round 1

[REV-0011](../reviews/M1-2-5-mapping-rule-target-profile-propagation-review.md) records `Request changes` against source head [`1cb85a81b00bce4729bfc2ce58ad871ab67ee1d0`](https://github.com/ThresholdOps/MotiveForce/commit/1cb85a81b00bce4729bfc2ce58ad871ab67ee1d0).

The architecture is retained. Corrections cover:

- complete candidate coverage and unsuccessful-evaluation provenance,
- separation of rule and ruleset capability requirements from actual compiler identity,
- compatibility and transformation authority and proof boundaries,
- replay-only use of `MAPPING_RULESET_UNRESOLVED`.

The corrected successor requires human semantic and design re-review under REV-0012. No acceptance or merge authorization is granted.

## Independent re-review and bounded correction

[REV-0012](../reviews/M1-2-5-mapping-rule-target-profile-propagation-review-2.md) records `Request changes` against semantic head [`7a6ec176a0fcc738a5c56a9c98a7d946446a2c01`](https://github.com/ThresholdOps/MotiveForce/commit/7a6ec176a0fcc738a5c56a9c98a7d946446a2c01).

The review retains the architecture and records:

- `REV12-FIND-001`: candidate-enumeration and filter-policy identity was not unambiguously closed as an immutable compilation and replay basis;
- `REV12-FIND-002`: current-compilation diagnostics had overlapping or incomplete trigger assignments.

The Proposed correction:

- makes one exact immutable candidate-enumeration policy revision a required member of each exact ruleset closure;
- introduces conceptual pre-evaluation `CandidateUniverseRecord` provenance for complete coverage reconciliation;
- propagates that exact basis through evaluation, compiler, replay, verification, partial-output, and Kernel-facing provenance;
- partitions current, replay, and verification diagnostics through one normative phase and precedence matrix using inherited codes only.

The bounded reviewer-attention clarification additionally:

- makes only the request-selected ruleset's directly owned enumeration policy operative across the complete imported closure while retaining imported policies as inert transitive identity and replay provenance;
- assigns mutable selectors, unresolved exact references, capability-blocked valid sources, and completed source assessments that cannot establish authoritative candidate-universe provenance to distinct phases and inherited diagnostics while retaining interrupted assessment as execution failure;
- makes `REPLAY_POLICY_UNRESOLVED` the sole primary code for absent policy identity or incomplete frozen parameters and limits `REPLAY_INPUT_CLOSURE_INCOMPLETE` to non-policy inputs and universe evidence after policy closure.

## Final human review

[REV-0013](../reviews/M1-2-5-mapping-rule-target-profile-propagation-review-3.md) records `Approve` against frozen semantic head [`f8d2249e4693305b57bf021c76bdd78b010da24b`](https://github.com/ThresholdOps/MotiveForce/commit/f8d2249e4693305b57bf021c76bdd78b010da24b).

The review:

- closes `REV12-FIND-001` and `REV12-FIND-002`;
- approves all three section 26.1 reviewer-attention clarifications;
- accepts all 15 design choices, including every Potential semantic change;
- approves the contract, DEC-0009, and M1.2.5 design-contract completion through merge of PR #26;
- authorizes bounded finalization and merge after validation without authorizing implementation.

## Related decisions

- [DEC-0005](../decisions/DEC-0005-record-envelope-revision-semantics.md), Accepted.
- [DEC-0006](../decisions/DEC-0006-deterministic-semantic-compiler-replay.md), Accepted.
- [DEC-0007](../decisions/DEC-0007-process-ir-diagnostic-severity-aggregation.md), Accepted.
- [DEC-0008](../decisions/DEC-0008-analyst-decision-staleness-revalidation.md), Accepted.
- [DEC-0009](../decisions/DEC-0009-mapping-rule-target-profile-propagation.md), Accepted through merge of PR #26.

## Deferred boundaries

- [Issue #6](https://github.com/ThresholdOps/MotiveForce/issues/6) remains open and not started.
- [Issue #8](https://github.com/ThresholdOps/MotiveForce/issues/8) retains detailed partial-compilation closure and remains not started.
- [Issue #9](https://github.com/ThresholdOps/MotiveForce/issues/9) retains BPMN metamodel-generation strategy and remains not started.
- [Issue #21](https://github.com/ThresholdOps/MotiveForce/issues/21) retains executable contract-test matrix work and remains not started.

Issue #9 does not block the bounded exact-reference, compatibility, and propagation design in M1.2.5.

## Outcome

Accepted and completed as design-contract work through merge of PR #26. REV-0013 closes both REV-0012 findings, approves the three section 26.1 clarifications, and authorizes bounded finalization and merge after validation. No runtime implementation is authorized or started.

## Follow-up

1. Merge [PR #26](https://github.com/ThresholdOps/MotiveForce/pull/26) after bounded-finalization validation and close Issue #20 after merge.
2. Keep M1.2 incomplete while Issue #8 and Issue #21 remain deferred.
3. Do not start runtime implementation or any deferred Issue through this finalization.
