# M1.2.1: RecordEnvelope and Revision Semantics Contract

- Milestone ID: `M1.2.1`
- Title: RecordEnvelope and Revision Semantics Contract
- Decision status: Accepted
- Milestone status: Completed
- Implementation status: Design contract completed; runtime implementation not started
- Tracking Issue: [Issue #16](https://github.com/ThresholdOps/MotiveForce/issues/16)
- Completed by [PR #22](https://github.com/ThresholdOps/MotiveForce/pull/22), branch `design/m1-2-1-record-envelope-revision-semantics`, squash-merged as [`034cdcd4c680d23bcd68b8ad959d0c4163532d9c`](https://github.com/ThresholdOps/MotiveForce/commit/034cdcd4c680d23bcd68b8ad959d0c4163532d9c).

## Objective

Define the accepted machine-readiness design contract for common Process IR record metadata, immutable revisions, revision lineage, supersession, exact-reference behavior, effective-status derivation, authorship versus authority, provenance, digest descriptors, revision-impact classification, and conservative authority carry-forward.

## Scope

- Accepted [RecordEnvelope contract](../../docs/PROCESS_IR_RECORD_ENVELOPE_CONTRACT.md).
- Accepted [DEC-0005](../decisions/DEC-0005-record-envelope-revision-semantics.md).
- Project-memory updates showing the conscious start of M1.2 through M1.2.1.
- Issue #16 update after Draft PR creation.
- Human review records [REV-0002](../reviews/M1-2-1-record-envelope-semantic-design-review.md), [REV-0003](../reviews/M1-2-1-record-envelope-semantic-design-review-2.md), and [REV-0004](../reviews/M1-2-1-record-envelope-semantic-design-review-3.md).

## Explicit non-goals

- No machine schema.
- No runtime implementation.
- No parser, compiler, BPMN Kernel, storage layer, transport API, executable validation, or tests.
- No implementation start for other M1.2 Issues.
- No confidential source material.

## Deliverables

- Accepted design contract: `docs/PROCESS_IR_RECORD_ENVELOPE_CONTRACT.md`.
- Accepted decision record: `project-memory/decisions/DEC-0005-record-envelope-revision-semantics.md`.
- Updated project-memory current state, scope, history, changelog, open items, glossary, and indexes.
- Updated Issue #16 with Draft PR linkage.

## Acceptance basis

Completion basis:

- human semantic and design acceptance recorded by [REV-0004](../reviews/M1-2-1-record-envelope-semantic-design-review-3.md),
- DEC-0005 is `Accepted`,
- the RecordEnvelope contract status is `Accepted`,
- completion is established through merge of PR #22.

M1.2.1 completion is design-contract completion only. Runtime implementation is not started.

## Review history

- First human semantic and design review completed against [`5fe3653a1ce5175841c843aa6d0196213e382341`](https://github.com/ThresholdOps/MotiveForce/commit/5fe3653a1ce5175841c843aa6d0196213e382341).
- Review outcome: Request changes.
- Canonical review record: [REV-0002](../reviews/M1-2-1-record-envelope-semantic-design-review.md).
- Corrections were applied in Draft PR #22.
- Second human semantic and design re-review completed against [`ed05f15dd42d95b3c38d56ae0ca19e39d783ee08`](https://github.com/ThresholdOps/MotiveForce/commit/ed05f15dd42d95b3c38d56ae0ca19e39d783ee08).
- Review outcome: Request changes.
- Canonical review record: [REV-0003](../reviews/M1-2-1-record-envelope-semantic-design-review-2.md).
- Three bounded corrections are being applied: reviewed preservation assertion authority and representation, generalized external exact bases, and current effective-status boundary while Issue #19 remains unresolved.
- Final human semantic and design review completed against [`b4c29bb8505db099feeb58afc3ec5755f90e85e8`](https://github.com/ThresholdOps/MotiveForce/commit/b4c29bb8505db099feeb58afc3ec5755f90e85e8).
- Review outcome: Approve.
- Canonical review record: [REV-0004](../reviews/M1-2-1-record-envelope-semantic-design-review-3.md).

M1.2.1 is `Accepted / Completed` through merge of PR #22. No runtime implementation is recorded.

## Related PRs

- [PR #22](https://github.com/ThresholdOps/MotiveForce/pull/22).

## Related commits

- Base `main` at [`caff0ba6f33cc0243d78dd61c091968a218a25f8`](https://github.com/ThresholdOps/MotiveForce/commit/caff0ba6f33cc0243d78dd61c091968a218a25f8).
- Initial PR #22 source head [`eb1472cd110fb6b601cfbfcb68553976343df969`](https://github.com/ThresholdOps/MotiveForce/commit/eb1472cd110fb6b601cfbfcb68553976343df969).
- Final PR #22 source head [`c969aa842ad4c4565eb7fcafd51b54d32c3520f4`](https://github.com/ThresholdOps/MotiveForce/commit/c969aa842ad4c4565eb7fcafd51b54d32c3520f4).
- Squash merge commit [`034cdcd4c680d23bcd68b8ad959d0c4163532d9c`](https://github.com/ThresholdOps/MotiveForce/commit/034cdcd4c680d23bcd68b8ad959d0c4163532d9c).

## Decisions created

- [DEC-0005](../decisions/DEC-0005-record-envelope-revision-semantics.md), Accepted.

## Outcome

Completed as an accepted design contract. No implementation has started.

## Follow-up

- Keep downstream schema work deferred to M2.
- Keep Issue #19 open for detailed AnalystDecision staleness, invalidation, revalidation, and controlled authority carry-forward policy.
- PR #22 squash merge provenance is synchronized by the M1.2.2 governance-affecting update.
