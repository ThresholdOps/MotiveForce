# DEC-0007: Process IR Diagnostic Severity and Aggregation Policy

- ID: `DEC-0007`
- Title: Process IR Diagnostic Severity and Aggregation Policy
- Status: Accepted
- Date: 2026-07-24T16:08:13Z
- Decision authority: Human final semantic and design approval in REV-0008; repository authority established through merge of PR #24
- Related Issue: [Issue #18](https://github.com/ThresholdOps/MotiveForce/issues/18)
- Related milestone: [M1.2.3](../milestones/M1-2-3-diagnostic-severity-aggregation.md)
- Source branch: `design/m1-2-3-diagnostic-policy`
- Source PR: [PR #24](https://github.com/ThresholdOps/MotiveForce/pull/24)
- Exact base: [`a63858354f6e34f7b56900dd5a89d04ac0b19cb5`](https://github.com/ThresholdOps/MotiveForce/commit/a63858354f6e34f7b56900dd5a89d04ac0b19cb5)
- Initial source head before self-provenance amend: [`36d2a0208651e87f83a16fe13b42ebaa7d7a8961`](https://github.com/ThresholdOps/MotiveForce/commit/36d2a0208651e87f83a16fe13b42ebaa7d7a8961)
- Human review round 1: [REV-0007](../reviews/M1-2-3-diagnostic-severity-aggregation-review.md), Request changes against [`8aadf16124bd354590c3e9457f4dc0228edea258`](https://github.com/ThresholdOps/MotiveForce/commit/8aadf16124bd354590c3e9457f4dc0228edea258)
- Human final review: [REV-0008](../reviews/M1-2-3-diagnostic-severity-aggregation-review-2.md), Approve against semantic head [`fe96e20bf927927fc6fd9e34b9c475b2ad0a1af4`](https://github.com/ThresholdOps/MotiveForce/commit/fe96e20bf927927fc6fd9e34b9c475b2ad0a1af4)
- Final source head: Recorded in PR #24 and Issue #18 metadata after the final amend; this record does not predict its own commit SHA

## Context

Accepted M1, M1.2.1, and M1.2.2 contracts define 76 unique diagnostic codes and defer a complete severity, blocking, aggregation, ordering, and outcome policy.

Later machine representation and implementation need a determinate design that preserves each accepted diagnostic meaning, scope-local refusal, partial-compilation behavior, exact revision boundaries, and replay comparison semantics.

## Decision

Accept:

- exactly `error`, `warning`, and `info` as normative severity values,
- severity and blocking as separate concepts,
- explicit operation-specific and scope-local blocking,
- `error` as the severity for all 76 inherited defect or unmet-condition diagnostics,
- semantic identity based on code, severity, blocking, exact affected records or scope, and semantic parameters,
- deduplication only for equal semantic projections,
- non-semantic multiplicity by default,
- deterministic non-semantic report ordering,
- compilation outcomes derived from blockers intersecting authoritative scope and dependency closure,
- same-policy replay reproduction of normative diagnostic severity and semantic projection,
- runtime execution failure as distinct from semantic refusal.

The complete accepted decision is defined by the [Diagnostic Policy Contract](../../docs/PROCESS_IR_DIAGNOSTIC_POLICY_CONTRACT.md).

## Accepted basis

- [M1 Process IR contract](../../docs/PROCESS_IR_CONTRACT.md)
- [M1.2.1 RecordEnvelope contract](../../docs/PROCESS_IR_RECORD_ENVELOPE_CONTRACT.md)
- [M1.2.2 replay contract](../../docs/SEMANTIC_COMPILER_REPLAY_CONTRACT.md)
- Accepted [DEC-0005](DEC-0005-record-envelope-revision-semantics.md)
- Accepted [DEC-0006](DEC-0006-deterministic-semantic-compiler-replay.md)
- Accepted M1 compilation and partial-compilation outcomes
- Accepted M1 business-semantic versus modeling-policy boundary
- Accepted M1.2.1 authority, revision, integrity, and current-status boundaries
- Accepted M1.2.2 semantic diagnostic comparison boundary

## Rationale

The accepted catalogues use blocking language but intentionally defer severity, aggregation, and ordering. Treating severity as blocking would make independent-fragment behavior ambiguous. Treating count or presentation order as semantic would introduce behavior unsupported by the accepted contracts.

The decision keeps the diagnostic collection semantic and order-independent while providing a deterministic report view. It extends the accepted M1.2.2 diagnostic projection through its explicit "at least" boundary by adding normative severity under the exact diagnostic policy.

`DIAG-CHOICE-001` remains historically classified as a potential semantic change because choosing a severity vocabulary is new normative policy. REV-0008 explicitly accepts it.

## Human review round 1

[REV-0007](../reviews/M1-2-3-diagnostic-severity-aggregation-review.md) records a completed human semantic and design review of source head `8aadf16124bd354590c3e9457f4dc0228edea258` with outcome `Request changes`.

The overall architecture is retained. The four bounded findings require:

- conjunctive evaluation of each accepted per-code blocking condition,
- mandatory deterministic ordering for an emitted report view while order remains non-semantic,
- `semantic mismatch` for unequal semantic diagnostic projections under the same exact comparable basis and policy,
- separate `not replayable` treatment for unresolved compiler identity and `not comparable` treatment for a changed exact compiler identity.

At the REV-0007 review stage, DEC-0007 remained `Proposed`; no acceptance or merge authorization was granted, and the corrected successor required human semantic and design re-review.

## Human review round 2

[REV-0008](../reviews/M1-2-3-diagnostic-severity-aggregation-review-2.md) records final human semantic and design approval of semantic head `fe96e20bf927927fc6fd9e34b9c475b2ad0a1af4`.

REV-0008 closes `REV7-FIND-001` through `REV7-FIND-004` and accepts:

- the three-level severity vocabulary,
- separation of severity and blocking,
- the complete 76-code registry,
- aggregation, deduplication, and non-semantic multiplicity,
- deterministic non-semantic report ordering,
- compilation outcome derivation,
- replay diagnostic compatibility and outcome boundaries,
- `DIAG-CHOICE-001` through `DIAG-CHOICE-010`.

DEC-0007 is accepted through merge of PR #24. No implementation authorization is granted.

## Alternatives considered

| Alternative | Status | Reason |
| --- | --- | --- |
| Treat every error as globally blocking. | Rejected in proposal. | Contradicts accepted scope-local partial compilation. |
| Derive outcome from highest severity. | Rejected in proposal. | Ignores authoritative scope and dependency closure. |
| Escalate repeated warnings to error. | Rejected in proposal. | No accepted count threshold or authority basis exists. |
| Treat every repeated instance as semantically distinct. | Rejected in proposal. | Explanation or emitter repetition does not change diagnostic meaning. |
| Deduplicate by code alone. | Rejected in proposal. | Different records, scopes, parameters, severity, or blocking are semantically different. |
| Make deterministic report order semantic. | Rejected in proposal. | Accepted replay rules exclude incidental ordering. |
| Add `fatal` or `critical`. | Rejected in proposal. | Runtime failure is not a higher semantic severity. |
| Define Issue #8, #19, or #20 trigger algorithms here. | Rejected in proposal. | Those are independently governed deferred outcomes. |

## Consequences

- Future machine schemas must represent severity and blocking separately.
- Future aggregation must retain complete provenance for collapsed duplicates.
- Compilation outcomes must use blockers and exact scope, not severity counts.
- Replay under the same diagnostic policy must reproduce the semantic diagnostic projection.
- Report order may be deterministic without becoming semantic.
- All 76 accepted source diagnostics remain unchanged and unique.
- Human review in REV-0008 accepts the severity vocabulary and registry fidelity.

## Dependencies and deferred boundaries

- [Issue #8](https://github.com/ThresholdOps/MotiveForce/issues/8): detailed partial-compilation dependency closure.
- [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19): staleness, invalidation, revalidation, and authority carry-forward triggers.
- [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20): mapping rules and target-profile propagation.
- [Issue #21](https://github.com/ThresholdOps/MotiveForce/issues/21): expanded contract-test matrix.
- M2: machine schema and executable validation.

M1.2.3 defines behavior when deferred-trigger diagnostics are emitted. It does not start or complete those Issues.

## Related artifacts

- [Diagnostic Policy Contract](../../docs/PROCESS_IR_DIAGNOSTIC_POLICY_CONTRACT.md)
- [M1.2 milestone](../milestones/M1-2-process-ir-machine-readiness.md)
- [M1.2.3 milestone](../milestones/M1-2-3-diagnostic-severity-aggregation.md)
- [Issue #18](https://github.com/ThresholdOps/MotiveForce/issues/18)

## Supersedes

None.

## Superseded by

None.

## Follow-up actions

- Complete M1.2.3 design-contract work through merge of PR #24.
- Close Issue #18 only after successful merge.
- Keep M1.2 as a whole Proposed, in progress, and not completed.
- Keep Issues #8 and #19-#21 open, deferred, and not started.
- Do not create schema, implementation, runtime, tests, or CI.

Acceptance is effective through merge of PR #24. This decision does not authorize implementation.
