# Project Memory

memory_schema_version: 1

Project memory is the repository-native governance layer for MøtiveFōrce. It records scope, decisions, rationale, history, reviews, risks, assumptions, and open questions in files that can be reviewed through pull requests.

## What belongs here

- Current-state summaries.
- Decision records with rationale and alternatives.
- Milestone records.
- Semantic review records.
- Project-definition and architecture changelog entries.
- Open decisions, risks, assumptions, and next actions.
- Links to repository artifacts supporting material claims.

## What does not belong here

- Runtime application memory.
- LLM vector stores.
- Knowledge graph implementation data.
- A replacement for Git history or GitHub PR discussions.
- Hidden chain-of-thought, private scratchpads, or unverifiable internal reasoning.
- Confidential documents, internal URLs, credentials, private source text, or personal data.

## Source-of-truth hierarchy

1. Merged repository content and merged decision records.
2. Accepted decision records under [decisions/](decisions/).
3. Current-state summaries.
4. Open pull requests and their reviewed content.
5. GitHub Issues as actionable-work records.
6. Conversation summaries and unverified notes.

Project memory summarizes and indexes authoritative artifacts. It does not override merged repository content. Draft content remains proposed until merged or explicitly accepted by an accepted decision record.

GitHub Issues track actionable work. An Issue may contain a proposal, investigation, or task, but it is not authoritative merely because it exists. Issues sit below accepted decisions and merged repository content in the source-of-truth hierarchy.

## Status vocabulary

- `Proposed`: drafted for review, not accepted.
- `Accepted`: adopted by merged repository content or an accepted decision record.
- `Rejected`: considered and declined.
- `Deferred`: intentionally postponed.
- `Superseded`: replaced by a later record.
- `In progress`: active but incomplete.
- `Completed`: completed according to repository evidence.
- `Blocked`: unable to proceed without a decision or external change.

A Draft PR does not make a decision `Accepted`. A merged PR may establish an accepted project decision if its content explicitly makes that decision.

Open work uses two independent status dimensions where relevant:

- Decision status: `Open`, `Proposed`, `Accepted`, `Rejected`, or `Deferred`.
- Implementation status: `Not started`, `Deferred in current phase`, `In progress`, `Blocked`, `Completed`, or `Not applicable`.

A decision may be `Open` while implementation is `Deferred in current phase`. Deferred implementation does not mean the decision has been made. `Deferred` as a decision status means the decision itself has intentionally been postponed. Project memory MUST NOT use one status to imply the other.

## Record ID conventions

- Decisions: `DEC-0001`
- History events: `HIST-0001`
- Changes: `CHG-0001`
- Milestones: `M0`, `M1`, `M1.1`, `M1.2`, `M1.2.1`, `M1.2.2`, `M1.2.3`, `M2`
- Reviews: `REV-0001`

IDs are never reused. Later records supersede earlier ones instead of silently rewriting them.

## Memory schema version

`memory_schema_version: 1` identifies the directory structure and record conventions used by `project-memory/`. It is adopted as the M1.1 project-memory governance profile by merge of [PR #3](https://github.com/ThresholdOps/MotiveForce/pull/3).

The memory schema version changes only when the structure or conventions of `project-memory/` itself change, not when record content changes. A structural change, such as a new required file, new record type, or new status value, is a governance decision and SHOULD be recorded as a decision record referencing the new schema version.

## Update rules

Governance-affecting changes MUST update the relevant `project-memory/` files in the same PR. This includes PRs that accept or change a decision, change project scope, materially change architecture, start, complete, block, or cancel a milestone, change governance conventions, or change the source-of-truth hierarchy.

Minor operational changes SHOULD update project memory in the same PR when the current-state or open-item record is materially affected. When they do not, the PR MUST link a complete follow-up Issue and record that tracking artifact.

This rule is not a blanket requirement to update project memory for every repository change. It applies to material governance changes and to operational changes that materially affect current state or tracked open work.

`CURRENT_STATE.md` MUST be re-verified against actual repository state at the start of any new milestone or governance-affecting PR. It must not be carried forward unchanged.

A milestone MUST NOT be recorded as `Completed` by project memory until the corresponding project-memory update has merged. If repository state already shows completion before project memory exists, the milestone record MUST say that the memory record itself is proposed until its PR merges.

If a governance-affecting merge occurs without a corresponding project-memory update, the gap MUST be recorded as `Unverified` in [OPEN_ITEMS.md](OPEN_ITEMS.md).

## Self-provenance rule

A project-memory PR cannot know its own future squash merge SHA before it merges.

Before merge, a project-memory PR MUST record the PR number, branch, source head SHA, base branch or base SHA where material, and reviewed state. The PR body should record the final source head after the last amend and push. Repository content MUST NOT invent or predict its own future squash merge SHA.

After merge, the actual merge SHA remains available from GitHub metadata. It SHOULD be recorded in the next governance-affecting project-memory PR when material. No immediate recursive PR is required solely to insert the previous project-memory PR's merge SHA. If no later governance PR occurs, GitHub PR metadata remains the authoritative merge record.

## GitHub Issue governance

Project memory records why work exists and how it relates to project decisions. GitHub Issues track the actionable work required to resolve, implement, investigate, or revisit it.

An actionable future or deferred item MUST NOT exist only as a bullet in project memory. It MUST have both:

1. a project-memory entry, and
2. a linked GitHub Issue with a complete description,

unless it is already actively tracked by an open pull request. An active pull request is a temporary exception only for work already underway. The project-memory entry MUST link to that PR and state that no separate Issue was created because the work is already active. If the active PR is closed without completing the work, a follow-up Issue MUST be created.

A GitHub Issue is REQUIRED for deferred implementation work, future capabilities requiring design or implementation, open architectural decisions requiring investigation or approval, semantic-review follow-up work, unresolved project-memory gaps, material risks requiring mitigation, governance changes requiring later execution, and tasks intentionally postponed to a later milestone.

A separate Issue is NOT required for glossary definitions, historical observations with no action, completed work, rejected work with no planned reconsideration, an item already being actively delivered by an open PR, or purely informational notes. When no Issue is required, the project-memory entry MUST state the reason.

Before opening an Issue, search open and closed Issues by likely title, concept, and related terminology. Reuse an existing Issue when scope and acceptance criteria are materially equivalent. Create a separate Issue only when the deliverable and acceptance criteria are independently meaningful.

Prefer one Issue per independently decidable or independently deliverable outcome. Group items only when they share the same objective, acceptance criteria, dependencies, and likely completion event.

New Issues created under this governance rule MUST use one of these title prefixes: `[Decision]`, `[Design]`, `[Implementation]`, `[Validation]`, `[Governance]`, or `[Risk]`. They MUST include complete sections for context, problem or decision required, why the work is not being done now, objective, scope, explicit non-goals, acceptance criteria, dependencies, related project-memory records, related artifacts, risks and constraints, evidence and provenance, suggested next step, and status.

## Issue lifecycle

When an Issue is opened, add or update the project-memory entry, link the Issue, and record decision and implementation statuses.

When an Issue changes materially, update project memory if scope changes, the decision outcome changes, implementation begins, a blocker appears, the Issue is split, or the Issue is superseded.

When an Issue closes, update project memory to record completion, rejection, duplication, supersession, or deferral. A closed Issue MUST NOT automatically mean work is completed; the closure reason must be reflected in project memory.

When an Issue is superseded, link the replacement Issue, retain the old Issue link, mark the project-memory item `Superseded`, and do not silently replace provenance.

## Stale-link governance

`CURRENT_STATE.md` MUST be reverified before a milestone or governance PR. Open-item Issue links SHOULD be checked during that verification. A missing, deleted, inaccessible, or inconsistent Issue link MUST be recorded as a project-memory gap. Project memory MUST NOT claim an Issue is open or closed without verification.

## Privacy and public repository constraints

This repository is public. Project memory MUST NOT include confidential company documents, proprietary source text, internal URLs, credentials, private access instructions, screenshots from internal systems, or personal data. Use synthetic or generalized descriptions.

## Navigation

- [Current State](CURRENT_STATE.md)
- [Scope](SCOPE.md)
- [History](HISTORY.md)
- [Changelog](CHANGELOG.md)
- [Open Items](OPEN_ITEMS.md)
- [Glossary](GLOSSARY.md)
- [Decisions](decisions/README.md)
- [DEC-0001: Canonical Semantic Model](decisions/DEC-0001-canonical-semantic-model.md)
- [DEC-0002: Agent, Compiler, Kernel Authority](decisions/DEC-0002-agent-compiler-kernel-authority.md)
- [DEC-0003: Process IR Before Kernel](decisions/DEC-0003-process-ir-before-kernel.md)
- [DEC-0004: Project Memory Governance](decisions/DEC-0004-project-memory-governance.md)
- [DEC-0005: Record Envelope and Revision Semantics](decisions/DEC-0005-record-envelope-revision-semantics.md)
- [DEC-0006: Deterministic Semantic Compiler Replay](decisions/DEC-0006-deterministic-semantic-compiler-replay.md)
- [DEC-0007: Process IR Diagnostic Severity and Aggregation Policy](decisions/DEC-0007-process-ir-diagnostic-severity-aggregation.md)
- [Milestones](milestones/README.md)
- [M0 Concept Definition](milestones/M0-concept-definition.md)
- [M1 Process IR Contract](milestones/M1-process-ir-contract.md)
- [M1.1 Project Memory Foundation](milestones/M1-1-project-memory-foundation.md)
- [M1.2 Process IR Machine-Readiness Hardening](milestones/M1-2-process-ir-machine-readiness.md)
- [M1.2.1 RecordEnvelope and Revision Semantics Contract](milestones/M1-2-1-record-envelope-revision-semantics.md)
- [M1.2.2 Deterministic Semantic Compiler Replay Contract](milestones/M1-2-2-deterministic-semantic-compiler-replay.md)
- [M1.2.3 Process IR Diagnostic Severity and Aggregation Policy](milestones/M1-2-3-diagnostic-severity-aggregation.md)
- [M2 Machine Schema and Contract Validation](milestones/M2-machine-schema-contract-validation.md)
- [Reviews](reviews/README.md)
- [M1 Process IR Semantic Review](reviews/M1-process-ir-semantic-review.md)
- [M1.2.1 RecordEnvelope Semantic and Design Review](reviews/M1-2-1-record-envelope-semantic-design-review.md)
- [M1.2.1 RecordEnvelope Semantic and Design Re-Review](reviews/M1-2-1-record-envelope-semantic-design-review-2.md)
- [M1.2.1 RecordEnvelope Final Semantic and Design Review](reviews/M1-2-1-record-envelope-semantic-design-review-3.md)
- [M1.2.2 Deterministic Semantic Compiler Replay Review](reviews/M1-2-2-deterministic-semantic-compiler-replay-review.md)
- [M1.2.2 Deterministic Semantic Compiler Replay Final Review](reviews/M1-2-2-deterministic-semantic-compiler-replay-review-2.md)
- [M1.2.3 Diagnostic Severity and Aggregation Review](reviews/M1-2-3-diagnostic-severity-aggregation-review.md)
- [M1.2.3 Diagnostic Severity and Aggregation Final Review](reviews/M1-2-3-diagnostic-severity-aggregation-review-2.md)
- [Decision Template](templates/decision-template.md)
- [Milestone Template](templates/milestone-template.md)
- [Review Template](templates/review-template.md)
- [Change Template](templates/change-template.md)

## How to start

A new contributor or agent should read, in order:

1. repository [README.md](../README.md),
2. [CURRENT_STATE.md](CURRENT_STATE.md),
3. [SCOPE.md](SCOPE.md),
4. relevant [decision records](decisions/README.md),
5. current [milestone](milestones/README.md) and [review](reviews/README.md) records,
6. [OPEN_ITEMS.md](OPEN_ITEMS.md).

Future agents MUST inspect repository state before trusting the current-state snapshot.
