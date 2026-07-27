# Current State

- Last verified: 2026-07-27T12:35:18Z
- Verification source: GitHub `main` at [`20f53f13938692b9c572b6f9f963e89fc22cb5b8`](https://github.com/ThresholdOps/MotiveForce/commit/20f53f13938692b9c572b6f9f963e89fc22cb5b8), merged [PR #25](https://github.com/ThresholdOps/MotiveForce/pull/25), closed [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19), open Issues [#6](https://github.com/ThresholdOps/MotiveForce/issues/6), [#8](https://github.com/ThresholdOps/MotiveForce/issues/8), [#9](https://github.com/ThresholdOps/MotiveForce/issues/9), [#20](https://github.com/ThresholdOps/MotiveForce/issues/20), and [#21](https://github.com/ThresholdOps/MotiveForce/issues/21), Draft [PR #26](https://github.com/ThresholdOps/MotiveForce/pull/26), accepted source contracts, accepted DEC-0005 through DEC-0008, REV-0001 through REV-0011, and `project-memory/`.

## Project status

MøtiveFōrce is `Concept / pre-MVP`.

No application, agent, semantic compiler, BPMN kernel, validator, user interface, or export adapter is implemented in merged repository content.

## Current architecture thesis

The canonical semantic model is the source of truth. BPMN diagrams, BPMN XML, BPMN DI, draw.io files, tables, RACI matrices, reports, and external-tool formats are projections.

The merged README states the boundary: the LLM interprets source material, the Semantic Compiler maps approved meaning, and the BPMN Kernel validates the resulting BPMN model.

## Merged milestones

- M0 concept definition: completed in repository history by [PR #1](https://github.com/ThresholdOps/MotiveForce/pull/1), merged at 2026-07-22T19:29:33Z with merge commit [`5c3350bde99fde4c3420902856d37a2800ebbea7`](https://github.com/ThresholdOps/MotiveForce/commit/5c3350bde99fde4c3420902856d37a2800ebbea7).
- M1 Process IR contract: completed by [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2), squash-merged at 2026-07-23T08:08:27Z with merge commit [`54d5e814601788574d13761561867ce5982cc88c`](https://github.com/ThresholdOps/MotiveForce/commit/54d5e814601788574d13761561867ce5982cc88c). The final source head was [`b2d6fe8f2192149145e04cbf2f0e5ffea737e1c0`](https://github.com/ThresholdOps/MotiveForce/commit/b2d6fe8f2192149145e04cbf2f0e5ffea737e1c0), and the merged document status is `Accepted`.
- M1.1 Project Memory Foundation: completed by [PR #3](https://github.com/ThresholdOps/MotiveForce/pull/3), squash-merged at 2026-07-23T11:06:24Z with merge commit [`caff0ba6f33cc0243d78dd61c091968a218a25f8`](https://github.com/ThresholdOps/MotiveForce/commit/caff0ba6f33cc0243d78dd61c091968a218a25f8). The final source head was [`71343343971c0a867fbade401f26503e87782cc1`](https://github.com/ThresholdOps/MotiveForce/commit/71343343971c0a867fbade401f26503e87782cc1), and project-memory governance is `Accepted`.

## Active milestone

- M1.2 Process IR Machine-Readiness Hardening: proposed and in progress at the design-program level. M1.2.1 through M1.2.4 are completed as design-contract work. M1.2.5 is the only active narrow design item. No runtime implementation has started, and M1.2 as a whole is not completed.
- M1.2.1 RecordEnvelope and Revision Semantics Contract: accepted and completed as design-contract work through [PR #22](https://github.com/ThresholdOps/MotiveForce/pull/22), squash-merged as [`034cdcd4c680d23bcd68b8ad959d0c4163532d9c`](https://github.com/ThresholdOps/MotiveForce/commit/034cdcd4c680d23bcd68b8ad959d0c4163532d9c). Human final review [REV-0004](reviews/M1-2-1-record-envelope-semantic-design-review-3.md) approved semantic head [`b4c29bb8505db099feeb58afc3ec5755f90e85e8`](https://github.com/ThresholdOps/MotiveForce/commit/b4c29bb8505db099feeb58afc3ec5755f90e85e8). Runtime implementation has not started.
- M1.2.2 Deterministic Semantic Compiler Replay Contract: accepted and completed as design-contract work through merge of [PR #23](https://github.com/ThresholdOps/MotiveForce/pull/23), squash commit [`a63858354f6e34f7b56900dd5a89d04ac0b19cb5`](https://github.com/ThresholdOps/MotiveForce/commit/a63858354f6e34f7b56900dd5a89d04ac0b19cb5). Human review [REV-0005](reviews/M1-2-2-deterministic-semantic-compiler-replay-review.md) requested one bounded correction; final review [REV-0006](reviews/M1-2-2-deterministic-semantic-compiler-replay-review-2.md) approved semantic head [`a411692f9a0b4ac754a1a0dd3cfbc3832ae3df08`](https://github.com/ThresholdOps/MotiveForce/commit/a411692f9a0b4ac754a1a0dd3cfbc3832ae3df08), closed `REV5-FIND-001`, and approved DEC-0006. Runtime implementation has not started.
- M1.2.3 Process IR Diagnostic Severity and Aggregation Policy: accepted and completed as design-contract work through merge of [PR #24](https://github.com/ThresholdOps/MotiveForce/pull/24), the accepted [Diagnostic Policy Contract](../docs/PROCESS_IR_DIAGNOSTIC_POLICY_CONTRACT.md), [DEC-0007](decisions/DEC-0007-process-ir-diagnostic-severity-aggregation.md), and the [M1.2.3 milestone](milestones/M1-2-3-diagnostic-severity-aggregation.md). [REV-0007](reviews/M1-2-3-diagnostic-severity-aggregation-review.md) requested four bounded corrections; [REV-0008](reviews/M1-2-3-diagnostic-severity-aggregation-review-2.md) approves semantic head [`fe96e20bf927927fc6fd9e34b9c475b2ad0a1af4`](https://github.com/ThresholdOps/MotiveForce/commit/fe96e20bf927927fc6fd9e34b9c475b2ad0a1af4) and closes all findings. No implementation has started.
- M1.2.4 AnalystDecision Staleness, Invalidation, Revalidation, and Controlled Authority Carry-Forward: accepted and completed as design-contract work through merge of [PR #25](https://github.com/ThresholdOps/MotiveForce/pull/25), the accepted [M1.2.4 contract](../docs/ANALYST_DECISION_STALENESS_REVALIDATION_CONTRACT.md), [DEC-0008](decisions/DEC-0008-analyst-decision-staleness-revalidation.md), [REV-0009](reviews/M1-2-4-analyst-decision-staleness-revalidation-review.md), final review [REV-0010](reviews/M1-2-4-analyst-decision-staleness-revalidation-review-2.md), and the [M1.2.4 milestone](milestones/M1-2-4-analyst-decision-staleness-revalidation.md). REV-0010 closes all findings and approves reviewed semantic head `4463aafca5e5fa176bcd3bb0db604b0a48943d9b`. No implementation has started.
- M1.2.5 Mapping Rule References, Ruleset Versioning, and Target BPMN Profile Propagation: Proposed and in progress for design only through [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20), Draft [PR #26](https://github.com/ThresholdOps/MotiveForce/pull/26), branch `design/m1-2-5-mapping-profile-propagation`, the Proposed [mapping/profile contract](../docs/MAPPING_RULE_TARGET_PROFILE_PROPAGATION_CONTRACT.md), [DEC-0009](decisions/DEC-0009-mapping-rule-target-profile-propagation.md), and [M1.2.5 milestone](milestones/M1-2-5-mapping-rule-target-profile-propagation.md). [REV-0011](reviews/M1-2-5-mapping-rule-target-profile-propagation-review.md) records Request changes against head [`1cb85a81b00bce4729bfc2ce58ad871ab67ee1d0`](https://github.com/ThresholdOps/MotiveForce/commit/1cb85a81b00bce4729bfc2ce58ad871ab67ee1d0); four bounded corrections are applied and human re-review under REV-0012 is required. No implementation has started.
- M2 Machine Schema and Contract Validation: proposed future milestone, implementation deferred in the current phase.

## Active governance work

- [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16) is closed as completed by PR #22 merge.
- [Issue #17](https://github.com/ThresholdOps/MotiveForce/issues/17) is completed through merge of [PR #23](https://github.com/ThresholdOps/MotiveForce/pull/23) and is closed after successful merge.
- [Issue #18](https://github.com/ThresholdOps/MotiveForce/issues/18) is closed as completed through merge of PR #24.
- [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19) is completed through merge of PR #25 and closed after successful merge.
- [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20) is open and consciously started as M1.2.5 design work.
- Other open Issues [#4](https://github.com/ThresholdOps/MotiveForce/issues/4)-[#15](https://github.com/ThresholdOps/MotiveForce/issues/15) and [#21](https://github.com/ThresholdOps/MotiveForce/issues/21) remain deferred or future work.

## M1.2.3 acceptance transition

- M1.2.3 accepts a three-level severity vocabulary, scope-local blocking, a complete registry of 76 diagnostic codes, semantic identity, aggregation, deterministic non-semantic ordering, and compilation/replay outcome derivation.
- [PR #24](https://github.com/ThresholdOps/MotiveForce/pull/24) uses branch `design/m1-2-3-diagnostic-policy`. Its initial source head before self-provenance amend is [`36d2a0208651e87f83a16fe13b42ebaa7d7a8961`](https://github.com/ThresholdOps/MotiveForce/commit/36d2a0208651e87f83a16fe13b42ebaa7d7a8961). The final source head remains in PR and Issue metadata; repository content does not predict its squash merge SHA.
- Human review [REV-0007](reviews/M1-2-3-diagnostic-severity-aggregation-review.md) requested four bounded corrections. Final review [REV-0008](reviews/M1-2-3-diagnostic-severity-aggregation-review-2.md) approves the corrected design, closes all findings, accepts DEC-0007, and authorizes completion through merge.

## M1.2.4 acceptance transition

- M1.2.4 accepts exact historical-validity and current-authority separation, an exact decision-basis closure, four derived current-authority outcomes, bounded staleness and invalidation rules, human revalidation, and non-transitive controlled carry-forward.
- [PR #25](https://github.com/ThresholdOps/MotiveForce/pull/25) uses branch `design/m1-2-4-analyst-decision-staleness`, based exactly on PR #24 squash merge [`006574b25732f0776a7e510fd33838c9946d9677`](https://github.com/ThresholdOps/MotiveForce/commit/006574b25732f0776a7e510fd33838c9946d9677). It was opened from initial source head [`377a6019afa65af9953e1f1dbcc8258416d94f50`](https://github.com/ThresholdOps/MotiveForce/commit/377a6019afa65af9953e1f1dbcc8258416d94f50).
- [REV-0009](reviews/M1-2-4-analyst-decision-staleness-revalidation-review.md) records `Request changes` against head `74d288fd57810f0b1a2c7865185889f07e67146e`. The architecture was retained and four bounded corrections were applied.
- [REV-0010](reviews/M1-2-4-analyst-decision-staleness-revalidation-review-2.md) records `Approve` against semantic head `4463aafca5e5fa176bcd3bb0db604b0a48943d9b`, closes all REV-0009 findings, accepts DEC-0008 and all ten design choices, and authorizes completion through merge.
- The contract, DEC-0008, and M1.2.4 are Accepted / Completed through merge of PR #25. No implementation is authorized.

## M1.2.5 conscious start

- M1.2.5 consumes accepted exact revision, replay, diagnostic, and current-authority foundations to define mapping-rule identity, exact ruleset closure, prerequisites, deterministic selection, exact target-profile identity, directional compatibility, explicit transformation, propagation, and provenance.
- The source branch is `design/m1-2-5-mapping-profile-propagation`, based exactly on PR #25 squash merge [`20f53f13938692b9c572b6f9f963e89fc22cb5b8`](https://github.com/ThresholdOps/MotiveForce/commit/20f53f13938692b9c572b6f9f963e89fc22cb5b8).
- The contract, DEC-0009, and M1.2.5 remain Proposed. Human semantic and design review is required.
- REV-0011 retained the architecture and requested four bounded corrections covering evaluation provenance, compiler identity, compatibility authority, and the replay-only ruleset diagnostic boundary.
- Issues #6, #8, #9, and #21 remain open and not started. No profile registry, metamodel, mapping engine, compiler, Kernel, schema, runtime, API, persistence, tests, or CI is created.

## Current blockers

- No current blocker is recorded for M0, M1, or M1.1.
- No current blocker is recorded for M1.2.1 design acceptance.
- No current blocker is recorded for M1.2.2 design acceptance.
- No current blocker is recorded for M1.2.3 design acceptance.
- No current blocker is recorded for M1.2.4 design acceptance.
- M1.2.5 requires human semantic and design re-review under REV-0012 before acceptance.

## Next expected decision

Human semantic and design re-review under REV-0012 of the corrected Proposed M1.2.5 contract and DEC-0009.

Tracking: [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20), branch `design/m1-2-5-mapping-profile-propagation`, [M1.2.5](milestones/M1-2-5-mapping-rule-target-profile-propagation.md), and [DEC-0009](decisions/DEC-0009-mapping-rule-target-profile-propagation.md). Issues #6, #8, #9, and #21 remain open and not started.

## Current out-of-scope areas

- Production application.
- Runtime agent.
- BPMN Kernel implementation.
- Machine-readable Process IR schema unless later approved.
- Knowledge graph implementation.
- Confidential source documents in the public repository.
- Runtime implementation of M1.2.1 concepts.
- Machine schema or executable validation for M1.2.1 concepts.
- Semantic Compiler implementation or runtime replay logging.
- Machine schema, executable replay verification, hashing algorithm, or canonical serialization for M1.2.2.
- Diagnostic engine, aggregation engine, machine schema, runtime logging, API, persistence, UI design, executable validation, tests, or CI for M1.2.3.
- Staleness engine, workflow engine, automatic authority agent, identity implementation, schema, runtime, API, persistence, UI, tests, or CI for M1.2.4.
- Mapping-rule implementation, rules engine, profile registry, generated metamodel, compiler or Kernel implementation, schema, parser, validator, runtime, API, persistence, UI, tests, or CI for M1.2.5.
