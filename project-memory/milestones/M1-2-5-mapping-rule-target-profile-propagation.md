# M1.2.5: Mapping Rule References, Ruleset Versioning, and Target BPMN Profile Propagation

- Milestone ID: `M1.2.5`
- Title: Mapping Rule References, Ruleset Versioning, and Target BPMN Profile Propagation Policy
- Decision status: Proposed
- Milestone status: Proposed
- Implementation status: In progress for design only
- Tracking Issue: [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20)
- Active branch: `design/m1-2-5-mapping-profile-propagation`
- Active Draft PR: [PR #26](https://github.com/ThresholdOps/MotiveForce/pull/26)
- Exact base: [`20f53f13938692b9c572b6f9f963e89fc22cb5b8`](https://github.com/ThresholdOps/MotiveForce/commit/20f53f13938692b9c572b6f9f963e89fc22cb5b8)
- Human semantic and design review round 1: [REV-0011](../reviews/M1-2-5-mapping-rule-target-profile-propagation-review.md), completed with Request changes against [`1cb85a81b00bce4729bfc2ce58ad871ab67ee1d0`](https://github.com/ThresholdOps/MotiveForce/commit/1cb85a81b00bce4729bfc2ce58ad871ab67ee1d0)
- Independent semantic and architectural re-review: [REV-0012](../reviews/M1-2-5-mapping-rule-target-profile-propagation-review-2.md), completed with Request changes against [`7a6ec176a0fcc738a5c56a9c98a7d946446a2c01`](https://github.com/ThresholdOps/MotiveForce/commit/7a6ec176a0fcc738a5c56a9c98a7d946446a2c01)
- Current correction status: `REV12-FIND-001` and `REV12-FIND-002` addressed by a Proposed correction pending human semantic and design re-review under REV-0013

## Objective

Define a bounded Proposed semantic and machine-readiness contract for exact, immutable, replayable, deterministic, profile-scoped Semantic Compiler mapping decisions.

## Scope

- logical mapping-rule identity,
- immutable mapping-rule revisions,
- exact `MappingRuleRef`,
- exact closed `MappingRulesetRef`,
- exact ruleset-owned candidate-enumeration policy and authoritative pre-evaluation candidate universe,
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

- Proposed [mapping and target-profile contract](../../docs/MAPPING_RULE_TARGET_PROFILE_PROPAGATION_CONTRACT.md).
- Proposed [DEC-0009](../decisions/DEC-0009-mapping-rule-target-profile-propagation.md).
- This milestone record.
- M1.2 parent and materially affected project-memory synchronization.
- Updated Issue #20 and Draft PR metadata.

## Accepted dependencies

- [M1 Process IR contract](../../docs/PROCESS_IR_CONTRACT.md).
- [M1.2.1 RecordEnvelope contract](../../docs/PROCESS_IR_RECORD_ENVELOPE_CONTRACT.md).
- [M1.2.2 replay contract](../../docs/SEMANTIC_COMPILER_REPLAY_CONTRACT.md).
- [M1.2.3 diagnostic policy](../../docs/PROCESS_IR_DIAGNOSTIC_POLICY_CONTRACT.md).
- [M1.2.4 staleness and revalidation contract](../../docs/ANALYST_DECISION_STALENESS_REVALIDATION_CONTRACT.md).
- DEC-0005 through DEC-0008.
- M1.2.1 through M1.2.4 Accepted / Completed status.

## Acceptance criteria

- [ ] Human semantic and design review is completed.
- [ ] Rule logical identity and immutable revision model are accepted.
- [ ] Exact ruleset identity, membership, imports, and closure are accepted.
- [ ] Prerequisite categories, dispositions, and satisfaction semantics are accepted.
- [ ] `MappingRuleApplication` and complete mapping provenance are accepted.
- [ ] Deterministic applicability, selection, precedence, equivalence, and fallback boundaries are accepted.
- [ ] Exact target-profile identity is accepted.
- [ ] Directional compatibility and explicit transformation semantics are accepted.
- [ ] Profile propagation across compiler, replay, and Kernel artifacts is accepted.
- [ ] Diagnostic and deferred-Issue boundaries are accepted.
- [ ] Contract status changes to Accepted through authorized finalization.
- [ ] DEC-0009 changes to Accepted through authorized finalization.
- [ ] Delivery PR is merged.
- [ ] Project memory is synchronized with completion.

None of these criteria is completed in this Draft delivery.

## Related PR

Draft [PR #26](https://github.com/ThresholdOps/MotiveForce/pull/26) was opened from initial source head [`1e874144aa68e444669a55913d44d1ab0dc73538`](https://github.com/ThresholdOps/MotiveForce/commit/1e874144aa68e444669a55913d44d1ab0dc73538). The final source head remains in PR and Issue metadata.

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

Both findings remain pending human semantic and design re-review under REV-0013. They are not closed by author correction. DEC-0009 and M1.2.5 remain Proposed, and no acceptance or merge authorization is granted.

## Related decisions

- [DEC-0005](../decisions/DEC-0005-record-envelope-revision-semantics.md), Accepted.
- [DEC-0006](../decisions/DEC-0006-deterministic-semantic-compiler-replay.md), Accepted.
- [DEC-0007](../decisions/DEC-0007-process-ir-diagnostic-severity-aggregation.md), Accepted.
- [DEC-0008](../decisions/DEC-0008-analyst-decision-staleness-revalidation.md), Accepted.
- [DEC-0009](../decisions/DEC-0009-mapping-rule-target-profile-propagation.md), Proposed.

## Deferred boundaries

- [Issue #6](https://github.com/ThresholdOps/MotiveForce/issues/6) remains open and not started.
- [Issue #8](https://github.com/ThresholdOps/MotiveForce/issues/8) retains detailed partial-compilation closure and remains not started.
- [Issue #9](https://github.com/ThresholdOps/MotiveForce/issues/9) retains BPMN metamodel-generation strategy and remains not started.
- [Issue #21](https://github.com/ThresholdOps/MotiveForce/issues/21) retains executable contract-test matrix work and remains not started.

Issue #9 does not block the bounded exact-reference, compatibility, and propagation design in M1.2.5.

## Outcome

Proposed and in progress for design only. REV-0012 requested two bounded changes; the Proposed correction awaits REV-0013 human semantic and design re-review. No implementation, acceptance, completion, or merge authorization is recorded.

## Follow-up

1. Complete validation of the Proposed corrections for `REV12-FIND-001` and `REV12-FIND-002`.
2. Obtain human semantic and design re-review under REV-0013 through Draft [PR #26](https://github.com/ThresholdOps/MotiveForce/pull/26).
3. Do not mark M1.2.5 complete or DEC-0009 Accepted in this delivery.
