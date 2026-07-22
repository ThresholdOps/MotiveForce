# DEC-0001: Canonical Semantic Model Is the Source of Truth

- ID: `DEC-0001`
- Title: Canonical semantic model is the source of truth
- Status: Accepted
- Date: 2026-07-22T19:29:33Z
- Decision authority: Merged repository content in [PR #1](https://github.com/ThresholdOps/MotiveForce/pull/1)

## Context

MøtiveFōrce needs to preserve process meaning, evidence, ambiguities, contradictions, and analytical decisions before producing diagrams or exchange formats.

## Decision

The canonical semantic model is the source of truth.

BPMN diagrams, BPMN XML, BPMN DI, draw.io files, tables, RACI matrices, reports, and external-tool formats are projections of that canonical model.

## Rationale

The merged [README.md](../../README.md) states that a BPMN diagram is a projection, not the source of truth, and identifies the canonical semantic process model as the source of truth.

## Alternatives considered

- Diagram as source of truth: rejected because it cannot preserve full evidence and ambiguity.
- XML as source of truth: rejected because XML is an exchange projection.
- Tables as source of truth: rejected because tables are generated projections.

## Consequences

- Future outputs must be generated from or linked back to canonical model state.
- Evidence and ambiguity cannot be treated as optional reporting details.
- Future schema and kernel work must preserve projection boundaries.

## Related artifacts

- [PR #1](https://github.com/ThresholdOps/MotiveForce/pull/1)
- Merge commit [`5c3350bde99fde4c3420902856d37a2800ebbea7`](https://github.com/ThresholdOps/MotiveForce/commit/5c3350bde99fde4c3420902856d37a2800ebbea7)
- Source commit [`0af0052c1e2504a944dea783b85cbba8ddf5ca6a`](https://github.com/ThresholdOps/MotiveForce/commit/0af0052c1e2504a944dea783b85cbba8ddf5ca6a)
- [README.md](../../README.md)

## Supersedes

None.

## Superseded by

None.

## Follow-up actions

- Keep projection documents and future implementation aligned with this source-of-truth boundary.
