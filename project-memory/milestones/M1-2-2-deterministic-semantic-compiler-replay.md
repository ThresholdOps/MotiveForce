# M1.2.2: Deterministic Semantic Compiler Replay Contract

- Milestone ID: `M1.2.2`
- Title: Deterministic Semantic Compiler Replay Contract
- Decision status: Accepted
- Milestone status: Completed
- Implementation status: Design contract completed; runtime implementation not started
- Tracking Issue: [Issue #17](https://github.com/ThresholdOps/MotiveForce/issues/17)
- Source branch: `design/m1-2-2-deterministic-compiler-replay`
- Delivery PR: [PR #23](https://github.com/ThresholdOps/MotiveForce/pull/23)
- Final review: [REV-0006](../reviews/M1-2-2-deterministic-semantic-compiler-replay-review-2.md), Approve against semantic head [`a411692f9a0b4ac754a1a0dd3cfbc3832ae3df08`](https://github.com/ThresholdOps/MotiveForce/commit/a411692f9a0b4ac754a1a0dd3cfbc3832ae3df08).

## Objective

Define the accepted conceptual contract required to reproduce and verify one Semantic Compiler execution without implementing the compiler, schema, runtime logging, hashing, executable validation, tests, or CI.

## Scope

- Core semantic replay invariant.
- Complete replay input closure.
- `CompilationReplayManifest`.
- `CompilerImplementationRef`.
- Replay requirement for exact `MappingRulesetRef`.
- `ReplayVerificationResult`.
- Semantic output equivalence without canonical byte identity.
- Minimum semantic comparison projection defined by the exact applicable replay-contract revision.
- Semantic identifier and diagnostic comparison boundaries.
- Observational metadata boundary.
- Nondeterminism controls.
- Historical replay versus current authority.
- Proposed replay diagnostics.
- Design-choice classifications, synthetic examples, and manual review tests.

## Explicit non-goals

- No Semantic Compiler implementation.
- No source extraction or LLM replay.
- No runtime logging or observability implementation.
- No machine schema or programming-language model.
- No persistence, API, or database design.
- No hashing algorithm or canonical serialization selection.
- No executable replay verification, tests, or CI.
- No start of Issues #8 or #18-#21.

## Deliverables

- Accepted [Semantic Compiler Replay Contract](../../docs/SEMANTIC_COMPILER_REPLAY_CONTRACT.md).
- Accepted [DEC-0006](../decisions/DEC-0006-deterministic-semantic-compiler-replay.md).
- Project-memory updates showing the conscious start and dependency boundaries of M1.2.2.
- [REV-0005](../reviews/M1-2-2-deterministic-semantic-compiler-replay-review.md), recording human Request changes and the bounded correction.
- [REV-0006](../reviews/M1-2-2-deterministic-semantic-compiler-replay-review-2.md), recording final human approval and finding closure.
- Issue #17 update with review, source-head, and completion provenance.

## Acceptance criteria

Completion requires:

- human semantic and design review,
- replay contract status changed to `Accepted`,
- DEC-0006 changed to `Accepted`,
- human review record linked,
- merge of PR #23,
- project-memory synchronization recording the accepted result.

These completion conditions are satisfied through REV-0006 and merge of PR #23. The status transition becomes repository-authoritative through that merge.

## Dependencies

- M1 is Accepted and Completed.
- M1.2.1 RecordEnvelope and revision semantics are Accepted and Completed.
- Issue #17 consumes exact revision, external basis, integrity, and historical/current authority rules from M1.2.1.
- Issue #18 owns detailed diagnostic severity and aggregation.
- Issue #8 owns detailed partial-compilation dependency closure.
- Issue #19 owns current-status staleness, invalidation, revalidation, and controlled carry-forward.
- Issue #20 consumes the replay requirements for exact mapping-ruleset and target-profile identity.

## Related PRs

- [PR #23](https://github.com/ThresholdOps/MotiveForce/pull/23) establishes the accepted M1.2.2 contract and project-memory changes through merge.

## Related commits

- Base `main`: [`034cdcd4c680d23bcd68b8ad959d0c4163532d9c`](https://github.com/ThresholdOps/MotiveForce/commit/034cdcd4c680d23bcd68b8ad959d0c4163532d9c).
- Initial PR #23 source head before self-provenance amend: [`d8142e36077a95edb98f5089919e47d59e35356f`](https://github.com/ThresholdOps/MotiveForce/commit/d8142e36077a95edb98f5089919e47d59e35356f).
- Final PR #23 source head: [`5c69345604c097e978f285d4be2cd85e1f397fb3`](https://github.com/ThresholdOps/MotiveForce/commit/5c69345604c097e978f285d4be2cd85e1f397fb3).
- Human-reviewed semantic head: [`a411692f9a0b4ac754a1a0dd3cfbc3832ae3df08`](https://github.com/ThresholdOps/MotiveForce/commit/a411692f9a0b4ac754a1a0dd3cfbc3832ae3df08).
- PR #23 squash merge: [`a63858354f6e34f7b56900dd5a89d04ac0b19cb5`](https://github.com/ThresholdOps/MotiveForce/commit/a63858354f6e34f7b56900dd5a89d04ac0b19cb5), synchronized by the next governance-affecting project-memory update.
- PR #22 final source and squash merge provenance are recorded by GitHub and synchronized in this governance update where material.

## Decisions created

- [DEC-0006](../decisions/DEC-0006-deterministic-semantic-compiler-replay.md), Accepted through merge of PR #23.

## Review history

- Human semantic and design review round 1 completed against [`7f70e0aeea17a0b1432bfb2c73ec496950f75ac7`](https://github.com/ThresholdOps/MotiveForce/commit/7f70e0aeea17a0b1432bfb2c73ec496950f75ac7).
- Outcome: `Request changes`.
- The overall replay architecture is retained.
- `REV5-FIND-001` requires a minimum semantic comparison projection.
- No acceptance or merge authorization was granted.
- Human semantic and design final re-review [REV-0006](../reviews/M1-2-2-deterministic-semantic-compiler-replay-review-2.md) approved corrected semantic head `a411692f...`.
- Outcome: `Approve`.
- `REV5-FIND-001`: Closed.
- The replay contract and DEC-0006 are accepted, and M1.2.2 is completed through merge of PR #23.

## Outcome

Completed as accepted design-contract work through merge of PR #23. No Semantic Compiler, Replay Verifier, schema, runtime logging, API, persistence, executable validation, tests, or CI has started.

## Follow-up

- Issue #17 is closed as completed after merge of PR #23.
- Issue #18 is consciously started separately as M1.2.3 diagnostic-policy design work.
- Keep Issues #8 and #19-#21 deferred and not started.
