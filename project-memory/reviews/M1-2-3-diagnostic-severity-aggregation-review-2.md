# REV-0008: M1.2.3 Diagnostic Severity and Aggregation Final Review

- Review ID: `REV-0008`
- Reviewed artifact: [docs/PROCESS_IR_DIAGNOSTIC_POLICY_CONTRACT.md](../../docs/PROCESS_IR_DIAGNOSTIC_POLICY_CONTRACT.md)
- Reviewed semantic head: [`fe96e20bf927927fc6fd9e34b9c475b2ad0a1af4`](https://github.com/ThresholdOps/MotiveForce/commit/fe96e20bf927927fc6fd9e34b9c475b2ad0a1af4)
- Review date: 2026-07-27T10:34:30Z
- Review type: Human semantic and design final re-review
- Reviewer authority: Human project semantic and design approval supplied with the finalization instruction
- Review status: Completed
- Review outcome: Approve
- Prior review: [REV-0007](M1-2-3-diagnostic-severity-aggregation-review.md)
- Decision effect: M1.2.3 design approved; DEC-0007 approved; merge authorized after bounded finalization validation; repository-authoritative acceptance becomes effective through merge of PR #24
- Implementation effect: None; implementation remains not started
- Related PR: [PR #24](https://github.com/ThresholdOps/MotiveForce/pull/24)
- Related Issue: [Issue #18](https://github.com/ThresholdOps/MotiveForce/issues/18)

## Approval provenance

Human semantic and design final re-review was performed against semantic head `fe96e20bf927927fc6fd9e34b9c475b2ad0a1af4`.

The later finalization amendment is limited to authorized review, status, governance, indexing, Issue, PR, and merge-preparation changes. No independent full semantic reread of that later amended source head is claimed.

Any normative semantic change beyond the reviewed head invalidates this approval and requires the delivery to stop.

## Review conclusions

### Severity vocabulary

Approved. The normative vocabulary is exactly `error`, `warning`, and `info`. No `fatal`, `critical`, numeric severity, score-based severity, or UI priority is accepted.

All 76 inherited diagnostic codes are accepted as `error` for their own affected conditions. `warning` and `info` remain available for later accepted non-blocking diagnostic definitions.

### Severity and blocking boundary

Approved. Severity and blocking are distinct. Every blocking diagnostic instance is `error`; `warning` and `info` never block.

An `error` may be non-blocking for an operation when its exact per-code trigger is inactive or its affected condition is outside the authoritative operation or dependency closure. Blocking requires all three:

1. the exact per-code blocking condition is active;
2. the exact diagnostic condition is present;
3. the condition intersects the authoritative operation or its required dependency closure.

### Diagnostic registry

Approved. The registry contains 35 M1 Process IR diagnostics, 29 M1.2.1 RecordEnvelope diagnostics, and 12 M1.2.2 replay diagnostics: 76 unique codes in total.

No code is added, removed, renamed, or duplicated. Per-code trigger conditions, scope behavior, outcome effects, semantic parameters, multiplicity, provenance, remediation authority, and deferred dependencies are accepted.

### Aggregation and deduplication

Approved. Semantic identity includes diagnostic code, severity, blocking status, affected exact record revisions, affected semantic scope, and semantic parameters.

Deduplication applies only to equal semantic projections. Collapsed duplicates retain all provenance, evidence, and originating record references. Multiplicity and counts are non-semantic and do not increase severity, blocking power, authority, or outcome effect.

### Report ordering

Approved. The semantic collection remains order-independent. When a report view is emitted under the exact policy, it must use the accepted deterministic order. Report ordering remains outside semantic equality and does not require canonical serialization.

### Compilation outcomes

Approved. Severity alone does not determine compilation outcome. `compiled`, `partially-compiled`, and `refused` derive from blocking diagnostic instances, authoritative scope, and required dependency closure.

Partial compilation remains explicitly enabled, scope-limited, incomplete, and unable to hide unresolved or excluded scope. Runtime execution failure remains distinct from semantic refusal.

### Replay compatibility

Approved. Under the same exact comparable basis and diagnostic policy, completed executions with different semantic diagnostic projections produce `semantic mismatch`.

Outcome boundaries remain distinct:

- changed exact basis: `not comparable`;
- missing, floating, incomplete, or unresolved basis: `not replayable`;
- runtime failure: `replay execution failed`;
- same exact comparable basis with unequal semantic output: `semantic mismatch`.

`COMPILER_IMPLEMENTATION_UNRESOLVED` applies only to missing, unavailable, mutable, or insufficient compiler identity and produces `not replayable`. Different available exact compiler identities use `REPLAY_NOT_COMPARABLE` and produce `not comparable`.

## Finding closure

| Finding ID | Final disposition | Basis |
| --- | --- | --- |
| `REV7-FIND-001` | Closed | Blocking now requires the exact per-code trigger, actual diagnostic condition, and authoritative-operation or dependency-closure intersection. |
| `REV7-FIND-002` | Closed | Emitted report views must use deterministic ordering while ordering remains non-semantic. |
| `REV7-FIND-003` | Closed | Same-policy comparable completed executions with unequal semantic diagnostic projections must produce semantic mismatch. |
| `REV7-FIND-004` | Closed | Unresolved compiler identity maps to not replayable; a different exact compiler identity maps to `REPLAY_NOT_COMPARABLE` and not comparable. |

No new finding IDs are created by REV-0008. No semantic blocker remains for M1.2.3.

## Design-choice decisions

- `DIAG-CHOICE-001` through `DIAG-CHOICE-010` are Accepted.
- `DIAG-CHOICE-001`, historically classified as a `Potential semantic change`, is explicitly accepted by this human review.
- The three-level severity vocabulary and all 76 inherited `error` assignments are Accepted.
- Severity and blocking separation, scope-local blocking, semantic diagnostic identity, non-semantic multiplicity, deterministic non-semantic ordering, compilation outcomes, replay severity reproduction, replay outcome boundaries, and the runtime-failure boundary are Accepted.

No implementation or algorithm selection is authorized.

## Decision effect

- Diagnostic Policy Contract: approved for acceptance through merge of PR #24.
- DEC-0007: approved for acceptance through merge of PR #24.
- M1.2.3: approved for completion as design-contract work through merge of PR #24.
- M1.2: remains Proposed, in progress, and not completed.
- Implementation: not started.
- Merge authorization: granted after bounded finalization validation.

## Deferred boundaries

Issues #8 and #19-#21 remain open, deferred, and not started. This approval does not authorize a Diagnostic Engine, Aggregation Engine, Replay Verifier, compiler implementation, schema, runtime logging, API, persistence, UI implementation, executable validation, tests, CI, hashing algorithm, or canonical serialization.
