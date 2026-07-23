# DEC-0005: Record Envelope and Revision Semantics

- ID: `DEC-0005`
- Title: Record envelope and revision semantics
- Status: Accepted
- Date: 2026-07-23T11:31:01Z
- Decision authority: Human final semantic and design approval recorded by [REV-0004](../reviews/M1-2-1-record-envelope-semantic-design-review-3.md); repository authority established through merge of [PR #22](https://github.com/ThresholdOps/MotiveForce/pull/22).
- Related Issue: [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16)
- Related milestone: [M1.2.1](../milestones/M1-2-1-record-envelope-revision-semantics.md)
- Accepted basis: accepted M1 contract plus [REV-0001](../reviews/M1-process-ir-semantic-review.md) qualification.
- Current review records: [REV-0002](../reviews/M1-2-1-record-envelope-semantic-design-review.md), [REV-0003](../reviews/M1-2-1-record-envelope-semantic-design-review-2.md), [REV-0004](../reviews/M1-2-1-record-envelope-semantic-design-review-3.md)
- Reviewed predecessor: [`5fe3653a1ce5175841c843aa6d0196213e382341`](https://github.com/ThresholdOps/MotiveForce/commit/5fe3653a1ce5175841c843aa6d0196213e382341)
- Second reviewed predecessor: [`ed05f15dd42d95b3c38d56ae0ca19e39d783ee08`](https://github.com/ThresholdOps/MotiveForce/commit/ed05f15dd42d95b3c38d56ae0ca19e39d783ee08)

## Context

M1 accepts the Process IR semantic boundary. Future machine-readiness work requires a common record envelope and revision model before machine schemas, deterministic replay, persistence, transport APIs, or migration can be designed safely.

REV-0001 qualifies the M1 acceptance provenance. M1.2.1 may define technical representation of accepted M1 semantics, but it must not silently reinterpret M1.

## Decision

Accepted decision:

- represent Process IR records through a common `RecordEnvelope` plus typed payload,
- distinguish logical record identity from immutable revision identity,
- require correction through new revisions rather than mutation,
- preserve same-record `RevisionLineage` and cross-record `RecordDerivationGraph` separately,
- require exact revision references for authoritative use by default, including revisioned authority, context, evidence, condition, rule, and policy bases,
- bind M1 four-axis value-state assessments to exact subject revisions, exact basis revisions, and applicable context,
- derive effective status from context, authority, lifecycle basis, and lineage,
- represent effective-status bases as separate revisioned records rather than mutating subject payload revisions,
- separate authorship from authority,
- define released revision as the immutability boundary while keeping edit buffers outside the contract,
- treat digests as integrity descriptors, not evidence or authority,
- classify revision impact,
- prevent automatic authority carry-forward to new revisions.

The first human review requested six correction areas: revision-scoped M1 four-axis value state, separation of `RevisionLineage` and `RecordDerivationGraph`, separation of subject revisions and status-basis revisions, authority carry-forward as a potential semantic change, released-revision immutability boundary, and exact references for all revisioned authoritative bases.

The second human review considered the REV-0002 findings materially addressed and retained the overall architecture. It requested three bounded corrections: authority and representation for reviewed preservation assertions, generalized exact references for external authoritative bases, and a current effective-status boundary while Issue #19 remains unresolved.

Semantic changes to accepted M1 require escalation. Conservative no-automatic-authority-carry-forward was classified as a historical `Potential semantic change` because escalation was required. It is accepted by REV-0004 as the M1.2.1 conservative default. Machine schema remains deferred to M2. Detailed `AnalystDecision` staleness, invalidation, revalidation, and controlled carry-forward policy remains tracked by [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19).

## Current review dispositions

- `REC-CHOICE-005`: Accepted by REV-0004 as the conservative default. No automatic authority or acceptance carry-forward occurs between revisions. Detailed controlled carry-forward remains deferred to Issue #19.
- `REC-CHOICE-009`: Accepted by REV-0004 with the reviewed preservation-assertion model.
- Generalized external exact bases: Accepted by REV-0004 for authoritative use across external authority, context, evidence, rule, condition, policy, mapping, source, and target-profile bases.
- Historical/current effective-status boundary: Accepted by REV-0004. Exact historical/as-of derivation is supported; authoritative current-status derivation remains bounded by the unresolved-staleness rule until Issue #19 defines an Accepted policy.

## Rationale

The accepted design model preserves auditability and makes revision behavior explicit before machine serialization. It avoids allowing an implementation detail such as storage, digest verification, or "latest revision" selection to create authority.

## Alternatives considered

| Alternative | Status | Reason |
| --- | --- | --- |
| Mutable records. | Rejected in proposal. | Mutation erases audit history and conflicts with M1 provenance discipline. |
| Logical ID only, without immutable revision IDs. | Rejected in proposal. | Exact review, decision, and compiler provenance would be unstable. |
| Automatic "latest revision" references. | Rejected in proposal. | Silent retargeting can change meaning after a decision or compilation request. |
| Automatic authority carry-forward. | Rejected in proposal. | Acceptance belongs to exact reviewed revisions unless a later accepted policy says otherwise. |
| Physical deletion of history. | Rejected in proposal. | Rejected, deferred, and superseded material must remain traceable. |
| Implicit four-axis inheritance. | Rejected in proposal. | Omission cannot establish that `knowledge_state`, `applicability`, `requirement_state`, and `value_presence` remain valid. |
| Cross-revision value-state composition. | Rejected in proposal. | Combining axes from different subject revisions would hide semantic basis changes. |
| One graph for revision lineage and record derivation. | Rejected in proposal. | Same-record effective revision selection and cross-record provenance have different semantics. |
| Subject-record mutation for status changes. | Rejected in proposal. | Effective status is derived from separate status-basis records. |
| Floating authority or context bases. | Rejected in proposal. | Exact subject references are insufficient if authority, context, or evidence floats. |
| Self-authorizing preservation metadata. | Rejected in proposal. | A preservation assertion must be a separate exact revisioned basis record or equivalent exact revisioned semantic record with authority where required. |
| Mutable external "current" references for authoritative bases. | Rejected in proposal. | External authoritative bases must be exact without inventing Process IR revision IDs for external artifacts. |
| Inferring current effective status from exact historical references alone. | Rejected in proposal. | Current authority requires an Accepted staleness and invalidation policy; historical/as-of derivation remains permitted. |

## Consequences

- M1.2.1 RecordEnvelope and revision semantics are accepted as design-contract work only.
- Later machine schema work must encode or validate immutable revision behavior.
- Future staleness and replay work must consume exact revision provenance.
- Conservative carry-forward requires later controlled policy work before any automated carry-forward behavior exists; that detailed policy remains Issue #19.
- This decision does not authorize schema, runtime, persistence, API, executable validation, tests, CI, or dependency changes.

## Related artifacts

- [M1 Process IR contract](../../docs/PROCESS_IR_CONTRACT.md)
- [M1.2.1 RecordEnvelope contract](../../docs/PROCESS_IR_RECORD_ENVELOPE_CONTRACT.md)
- [REV-0001](../reviews/M1-process-ir-semantic-review.md)
- [REV-0002](../reviews/M1-2-1-record-envelope-semantic-design-review.md)
- [REV-0003](../reviews/M1-2-1-record-envelope-semantic-design-review-2.md)
- [REV-0004](../reviews/M1-2-1-record-envelope-semantic-design-review-3.md)
- [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16)
- [PR #22](https://github.com/ThresholdOps/MotiveForce/pull/22)
- [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19)
- [Issue #5](https://github.com/ThresholdOps/MotiveForce/issues/5)

## Supersedes

None.

## Superseded by

None.

## Follow-up actions

- Keep schema representation deferred to M2.
- Keep Issue #19 open for detailed staleness, invalidation, revalidation, and controlled carry-forward policy.
- Synchronize the PR #22 squash merge SHA in a later governance-affecting project-memory update if material.
