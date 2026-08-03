# Decision Records

Decision records preserve governance decisions, rationale, alternatives, consequences, and provenance.

## Status lifecycle

Decision statuses are `Proposed`, `Accepted`, `Rejected`, `Deferred`, and `Superseded`.

A Draft PR can contain a `Proposed` decision. A decision becomes `Accepted` only through merged repository content or a later accepted decision record. A later decision must not silently rewrite an earlier one; it must supersede, amend, or leave the earlier record unchanged.

## Numbering convention

Decision IDs use `DEC-0001`, `DEC-0002`, and so on. IDs are never reused.

## Required metadata

Each decision record contains:

- ID
- Title
- Status
- Date
- Decision authority
- Context
- Decision
- Rationale
- Alternatives considered
- Consequences
- Related artifacts
- Supersedes
- Superseded by
- Follow-up actions

Decision records for governance-affecting PRs should also identify source PR, branch, source head SHA, and merge SHA where available. A decision record must not predict the future squash merge SHA of the PR that introduces it.

## Decision records versus current state

Decision records are historical governance records. [CURRENT_STATE.md](../CURRENT_STATE.md) is a mutable summary. If they disagree, inspect merged repository content and decision provenance before updating either file.

## How to add a decision

Create a new `DEC-####-short-title.md` file from [decision-template.md](../templates/decision-template.md). Link the PR, commits, and source files that support the decision.

## How to supersede a decision

Create a new decision record, set the old record's `Superseded by` field in the same PR when appropriate, and explain what changed. Do not reuse the old ID.

## Current records

- [DEC-0001: Canonical Semantic Model](DEC-0001-canonical-semantic-model.md)
- [DEC-0002: Agent, Compiler, and Kernel Authority](DEC-0002-agent-compiler-kernel-authority.md)
- [DEC-0003: Process IR Before Kernel](DEC-0003-process-ir-before-kernel.md)
- [DEC-0004: Project Memory Governance](DEC-0004-project-memory-governance.md)
- [DEC-0005: Record Envelope and Revision Semantics](DEC-0005-record-envelope-revision-semantics.md), Accepted.
- [DEC-0006: Deterministic Semantic Compiler Replay](DEC-0006-deterministic-semantic-compiler-replay.md), Accepted through merge of PR #23.
- [DEC-0007: Process IR Diagnostic Severity and Aggregation Policy](DEC-0007-process-ir-diagnostic-severity-aggregation.md), Accepted through merge of PR #24.
- [DEC-0008: AnalystDecision Staleness, Invalidation, Revalidation, and Controlled Authority Carry-Forward](DEC-0008-analyst-decision-staleness-revalidation.md), Accepted through merge of PR #25; REV-0010 closes all REV-0009 findings.
- [DEC-0009: Mapping Rule References and Target BPMN Profile Propagation](DEC-0009-mapping-rule-target-profile-propagation.md), Accepted through merge of PR #26; REV-0013 closes both REV-0012 findings and approves all three section 26.1 clarifications.
- [DEC-0010: Structured Elicitation Extraction](DEC-0010-structured-elicitation-extraction.md), Proposed in the M1.2.6 Draft work; separate human semantic review required.
