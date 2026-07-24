# REV-0006: M1.2.2 Deterministic Semantic Compiler Replay Final Review

- Review ID: `REV-0006`
- Reviewed artifact: [docs/SEMANTIC_COMPILER_REPLAY_CONTRACT.md](../../docs/SEMANTIC_COMPILER_REPLAY_CONTRACT.md)
- Reviewed semantic head: [`a411692f9a0b4ac754a1a0dd3cfbc3832ae3df08`](https://github.com/ThresholdOps/MotiveForce/commit/a411692f9a0b4ac754a1a0dd3cfbc3832ae3df08)
- Review date: 2026-07-24T15:31:13Z
- Review type: Human semantic and design final re-review
- Reviewer authority: Human project semantic and design approval supplied with the finalization instruction
- Review status: Completed
- Review outcome: Approve
- Prior review: [REV-0005](M1-2-2-deterministic-semantic-compiler-replay-review.md)
- Decision effect: M1.2.2 design approved; DEC-0006 approved; merge authorized after bounded finalization validation; repository-authoritative acceptance becomes effective through merge of PR #23
- Implementation effect: None; implementation remains not started
- Related PR: [PR #23](https://github.com/ThresholdOps/MotiveForce/pull/23)
- Related Issue: [Issue #17](https://github.com/ThresholdOps/MotiveForce/issues/17)

## Provenance qualification

The human semantic and design final re-review was performed against semantic head `a411692f9a0b4ac754a1a0dd3cfbc3832ae3df08`.

This record memorializes the human approval supplied with the finalization instruction. It is not an author self-review.

The later bounded finalization amendment is authorized only for this review record, acceptance status, finding closure, governance synchronization, indexing, PR and Issue metadata, and merge preparation. No independent full semantic reread of that later amended source head is claimed.

Any normative semantic change beyond the reviewed head invalidates this approval and MUST stop the delivery.

## Review conclusions

### Semantic projection

Approved.

The exact applicable replay-contract revision defines the comparison projection. The projection sufficiently covers, where applicable:

- compilation outcome,
- requested scope,
- authoritative compiled scope,
- non-authoritative scope,
- excluded scope,
- unresolved scope,
- semantic BPMN graph,
- semantic model and element identities,
- semantic element types,
- connections and relations,
- sequence-flow conditions,
- participant and lane boundaries,
- activity semantics,
- event semantics,
- exact source-revision provenance,
- mapping-rule references and provenance,
- target BPMN profile,
- semantic diagnostic projection.

Serialization layout, byte layout, graph traversal order, presentation formatting, runtime state, and observational metadata remain outside semantic equality.

### Identifier boundary

Approved.

Semantic equality includes only identifiers defined as semantic identity of `CompiledSemanticModel` or its semantic elements.

Serialization node IDs, database IDs, runtime object IDs, memory addresses, temporary container IDs, execution IDs, run IDs, trace IDs, and log correlation IDs remain excluded by default.

Generated semantic identifiers must be deterministic from exact inputs and exact policy, or preserved only when they were genuine inputs to the original compilation. Original output identifiers may not be injected into replay solely to force equality.

No identifier-generation algorithm is accepted or selected.

### Diagnostic comparison projection

Approved.

The minimum semantic diagnostic projection includes:

- diagnostic code,
- blocking status,
- affected exact records or semantic scope,
- semantic parameters determining diagnostic meaning.

Free-text explanations, remediation wording, localization, formatting, timestamps, log metadata, trace metadata, and incidental ordering are non-semantic by default. Order and multiplicity become semantically significant only when the exact diagnostic policy defines them that way.

Issue #18 remains responsible for final severity vocabulary, blocking policy details, aggregation, ordering, deduplication, multiplicity, and outcome derivation. Issue #18 remains open and not started.

### Comparison authority

Approved.

A future deterministic implementation evaluating the contract would have replay-comparison authority only. It would not establish business truth, evidence validity, current authority, current acceptance, BPMN validity, or `AnalystDecision` validity.

No Replay Verifier subsystem is authorized or created.

## Finding closure

| Finding ID | Final disposition | Basis |
| --- | --- | --- |
| `REV5-FIND-001` | Closed | The corrected contract defines an exact replay-contract-revision-scoped semantic projection, the semantic identifier boundary, minimum diagnostic projection, comparison basis, serialization boundary, examples, and manual tests. |

No new finding IDs are created by REV-0006.

## Design-choice decisions

- `REPLAY-CHOICE-001` through `REPLAY-CHOICE-010` are Accepted as part of the approved M1.2.2 contract.
- `REPLAY-CHOICE-003` remains correctly classified as M1.2.1-derived.
- `REPLAY-CHOICE-004` is Accepted: semantic equivalence is evaluated using the projection defined by the exact applicable replay-contract revision; canonical byte identity remains deferred.
- `REPLAY-CHOICE-009` is Accepted as a semantic identifier boundary.
- Acceptance of `REPLAY-CHOICE-009` does not select an identifier-generation or hashing algorithm.
- `REPLAY-CHOICE-010` is Accepted only as the requirement for an exact diagnostic-policy reference where policy affects replay output.
- Complete diagnostic-policy design remains assigned to Issue #18.

## Deferred non-blocking topics

The following remain non-blocking and deferred:

- Replay Verifier architecture,
- standalone comparison-policy artifact,
- manifest lifecycle and reconstruction implementation,
- dependency-role schema,
- complete identifier taxonomy,
- identifier-generation algorithm,
- canonical serialization,
- complete diagnostic policy,
- executable comparison logic,
- runtime logging,
- persistence,
- API,
- schema,
- tests and CI.

These topics are not findings in REV-0006.

## Final disposition

- REV5-FIND-001: Closed.
- Semantic projection: Accepted.
- Semantic identifier boundary: Accepted.
- Diagnostic comparison projection: Accepted and compatible with future Issue #18 policy.
- Design ready for acceptance: Yes.
- Replay contract: Approved, effective as repository-authoritative content through merge of PR #23.
- DEC-0006: Approved, effective as repository-authoritative content through merge of PR #23.
- M1.2.2: Approved for completion through merge of PR #23.
- Merge authorization: Granted after bounded finalization validation.
- Implementation authorization: None.
