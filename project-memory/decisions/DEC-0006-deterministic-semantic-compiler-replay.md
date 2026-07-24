# DEC-0006: Deterministic Semantic Compiler Replay

- ID: `DEC-0006`
- Title: Deterministic Semantic Compiler replay
- Status: Accepted
- Date: 2026-07-24T11:14:31Z
- Decision authority: Human final semantic and design approval recorded by [REV-0006](../reviews/M1-2-2-deterministic-semantic-compiler-replay-review-2.md); repository authority is established through merge of [PR #23](https://github.com/ThresholdOps/MotiveForce/pull/23).
- Related Issue: [Issue #17](https://github.com/ThresholdOps/MotiveForce/issues/17)
- Related milestone: [M1.2.2](../milestones/M1-2-2-deterministic-semantic-compiler-replay.md)
- Final review: [REV-0006](../reviews/M1-2-2-deterministic-semantic-compiler-replay-review-2.md), Approve against semantic head [`a411692f9a0b4ac754a1a0dd3cfbc3832ae3df08`](https://github.com/ThresholdOps/MotiveForce/commit/a411692f9a0b4ac754a1a0dd3cfbc3832ae3df08).
- Accepted basis: accepted [M1 contract](../../docs/PROCESS_IR_CONTRACT.md), accepted [M1.2.1 contract](../../docs/PROCESS_IR_RECORD_ENVELOPE_CONTRACT.md), [DEC-0005](DEC-0005-record-envelope-revision-semantics.md), and [REV-0004](../reviews/M1-2-1-record-envelope-semantic-design-review-3.md).

## Context

M1 defines a deterministic Semantic Compiler boundary. M1.2.1 establishes immutable record revisions, exact authoritative bases, integrity descriptors, historical/as-of derivation, and the boundary around current effective status.

The project now needs a design contract identifying everything required to reproduce and verify one Semantic Compiler execution before machine schema, compiler implementation, runtime logging, or executable validation begins.

## Decision

Accepted decision:

- define `CompilationReplayManifest` as the complete exact replay-affecting input closure,
- require immutable compiler implementation identity rather than a version label alone,
- require exact mapping-ruleset and target-profile identities for replay,
- compare the minimum semantic projection defined by the exact applicable replay-contract revision without claiming canonical byte identity,
- include semantic model and element identities while excluding serialization, runtime, and observational identifiers from semantic equality,
- compare diagnostic code, blocking status, affected exact scope, and semantic parameters under the exact diagnostic policy,
- distinguish replay-affecting inputs from observational metadata,
- control nondeterminism by forbidding, freezing, normalizing, or excluding each potential influence,
- treat changed compiler, ruleset, policy, or profile executions as regression, migration, or compatibility comparisons rather than verification of the same replay claim,
- preserve the accepted rule that historical reproducibility does not establish current authority,
- reuse M1.2.1 integrity descriptors without treating digests as evidence or authority,
- depend on separate future contracts for diagnostic policy, partial-compilation dependency closure, current-status staleness, and detailed mapping/profile propagation.

The exact accepted decision is defined in the [Semantic Compiler Replay Contract](../../docs/SEMANTIC_COMPILER_REPLAY_CONTRACT.md).

This decision is Accepted through merge of PR #23. REV-0005 retained the architecture and requested one bounded semantic-comparison correction; REV-0006 approved the corrected semantic head and closed `REV5-FIND-001`.

## Rationale

Determinism cannot be verified from output alone or from mutable labels. Replay requires a closed, exact record of every semantic, policy, implementation, mapping, profile, and execution input that can affect compiler output.

Semantic equivalence is used because the project has not accepted a canonical machine serialization. This allows design review of deterministic compiler behavior without inventing byte-level guarantees.

The exact replay-contract revision defines the comparison projection. This avoids both an underspecified comparison and a separate comparison-policy architecture. Semantic identifiers and semantic diagnostic fields are compared; serialization, presentation, and observational differences are excluded unless a future Accepted contract makes them semantic.

The proposal keeps source interpretation and the LLM outside replay, preserves the Semantic Compiler and BPMN Kernel authority boundary, and prevents historical reproducibility from being confused with current business authority.

## Review history

- [REV-0005](../reviews/M1-2-2-deterministic-semantic-compiler-replay-review.md) reviewed source head [`7f70e0aeea17a0b1432bfb2c73ec496950f75ac7`](https://github.com/ThresholdOps/MotiveForce/commit/7f70e0aeea17a0b1432bfb2c73ec496950f75ac7).
- Outcome: `Request changes`.
- Overall architecture: retained.
- Finding `REV5-FIND-001`: define the minimum semantic comparison projection.
- No Replay Verifier subsystem, standalone comparison-policy artifact, manifest lifecycle redesign, dependency-role schema, or complete identifier taxonomy was required by the review.
- [REV-0006](../reviews/M1-2-2-deterministic-semantic-compiler-replay-review-2.md) reviewed corrected semantic head [`a411692f9a0b4ac754a1a0dd3cfbc3832ae3df08`](https://github.com/ThresholdOps/MotiveForce/commit/a411692f9a0b4ac754a1a0dd3cfbc3832ae3df08).
- Outcome: `Approve`.
- `REV5-FIND-001`: Closed.
- Semantic projection, identifier boundary, diagnostic projection, and comparison-authority boundary: Accepted.
- `REPLAY-CHOICE-001` through `REPLAY-CHOICE-010`: Accepted as part of this decision.
- The finalization amendment is governance-only and does not claim an independent full semantic reread after `a411692f...`.

## Alternatives considered

| Alternative | Status | Reason |
| --- | --- | --- |
| Identify the compiler by human-readable version label only. | Rejected in proposal. | A label may identify multiple builds or dependency sets and cannot prove identical semantic behavior. |
| Resolve replay dependencies through mutable `latest` or `current` selectors. | Rejected in proposal. | Silent retargeting destroys historical reproducibility. |
| Require byte identity as the only replay criterion. | Rejected in proposal. | No canonical serialization is accepted; byte differences can be observational or represent equivalent graph ordering. |
| Replay the LLM interpretation stage. | Rejected in proposal. | M1 places probabilistic interpretation before the deterministic Semantic Compiler boundary. |
| Allow uncaptured environment dependencies. | Rejected in proposal. | Locale, time, ordering, services, or environment could silently alter output. |
| Treat compiler upgrades as verification of the same replay. | Rejected in proposal. | A changed compiler is a regression, migration, or compatibility comparison. |
| Use matching digests as evidence or authority. | Rejected in proposal. | Digests support integrity and do not establish business truth or authorization. |
| Store only outputs without complete input closure. | Rejected in proposal. | Output alone cannot identify why it was produced or reproduce it. |

## Consequences

- Future replay implementations must expose the complete replay-affecting basis set.
- Future compiler implementation identity must be immutable and sufficiently complete for semantic comparison.
- Issue #20 must consume exact mapping-ruleset and target-profile replay requirements.
- Issue #18 remains responsible for diagnostic severity, blocking, aggregation, and stable ordering.
- Issue #8 remains responsible for detailed partial-compilation dependency closure.
- Issue #19 remains responsible for current-status staleness, invalidation, revalidation, authority expiry, and controlled carry-forward.
- M2 remains responsible for machine schema, canonical representation decisions, and executable contract validation.
- No compiler, schema, runtime logging, API, persistence, hashing algorithm, tests, CI, or dependency work is authorized.

## Related artifacts

- [M1 Process IR contract](../../docs/PROCESS_IR_CONTRACT.md)
- [M1.2.1 RecordEnvelope contract](../../docs/PROCESS_IR_RECORD_ENVELOPE_CONTRACT.md)
- [M1.2.2 replay contract](../../docs/SEMANTIC_COMPILER_REPLAY_CONTRACT.md)
- [DEC-0005](DEC-0005-record-envelope-revision-semantics.md)
- [REV-0004](../reviews/M1-2-1-record-envelope-semantic-design-review-3.md)
- [REV-0005](../reviews/M1-2-2-deterministic-semantic-compiler-replay-review.md)
- [REV-0006](../reviews/M1-2-2-deterministic-semantic-compiler-replay-review-2.md)
- [M1.2 milestone](../milestones/M1-2-process-ir-machine-readiness.md)
- [M1.2.2 milestone](../milestones/M1-2-2-deterministic-semantic-compiler-replay.md)
- [Issue #17](https://github.com/ThresholdOps/MotiveForce/issues/17)
- [Issue #18](https://github.com/ThresholdOps/MotiveForce/issues/18)
- [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19)
- [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20)
- [Issue #8](https://github.com/ThresholdOps/MotiveForce/issues/8)

## Dependencies

- Accepted M1 Semantic Compiler boundary.
- Accepted M1.2.1 exact revision, external basis, integrity, and historical/current authority rules.
- Detailed downstream policy remains deferred to Issues #8, #18, #19, and #20.

## Supersedes

None.

## Superseded by

None.

## Follow-up actions

- Close Issue #17 after successful merge of PR #23.
- Keep Issues #8 and #18-#21 deferred and not started.
- Treat Issue #18 as a possible next candidate for a separate conscious start without starting it through this decision.
- Do not begin compiler implementation, Replay Verifier work, runtime logging, schema, API, persistence, executable replay verification, tests, or CI through this decision.
