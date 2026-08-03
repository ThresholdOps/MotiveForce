# DEC-0011: Merge Strategy for Reviewed and Bounded-Finalization PRs

- ID: `DEC-0011`
- Title: Merge strategy for exact-head-reviewed and bounded-finalization pull requests
- Status: Accepted through merge of PR #30
- Date: 2026-08-03
- Decision authority: The project owner personally reviewed exact head [`e0020a44b0b649b711402d282d4cf5ece31708a8`](https://github.com/ThresholdOps/MotiveForce/commit/e0020a44b0b649b711402d282d4cf5ece31708a8), approved Option A with no findings, authorized bounded finalization within a closed allowlist, and authorized merge after successful validation in the [human governance decision](https://github.com/ThresholdOps/MotiveForce/pull/30#issuecomment-5165269810). Acceptance is completed through merge of PR #30.
- Tracking Issue: [Issue #28](https://github.com/ThresholdOps/MotiveForce/issues/28), `OPEN-0021`
- Source PR: [PR #30](https://github.com/ThresholdOps/MotiveForce/pull/30)
- Source branch: `agent/merge-strategy-governance`
- Exact base: [`2387307f2f7a3f05b65197497b9f0945bb26bf6a`](https://github.com/ThresholdOps/MotiveForce/commit/2387307f2f7a3f05b65197497b9f0945bb26bf6a)
- Related active design PR: [PR #29](https://github.com/ThresholdOps/MotiveForce/pull/29), unchanged by this finalization

## Context

PR #26 exposed a repository-history governance gap. Human review approved exact semantic head `f8d2249e4693305b57bf021c76bdd78b010da24b`. Bounded finalization produced head `04d1db644bab4ab0e30973cda57a57d6065ec019`. Squash merge produced `2387307f2f7a3f05b65197497b9f0945bb26bf6a` on `main`, leaving neither reviewed nor finalization head as an ancestor of `main`.

PR #26 retained provenance through its description, REV-0013, project-memory records, and the project owner's human-attestation comment in Issue #20. That compensation was effective, but the choice between squash and merge commit was made at the end of the workflow rather than governed in advance.

DEC-0004 defines where project governance is recorded, how self-provenance is handled, and why a PR must not predict its own future merge SHA. It does not decide merge topology. This proposal therefore extends DEC-0004 without amending or superseding it.

Issue #28 gates REV-0014 on resolving this rule before review evidence is frozen or review begins.

## Scope

This decision applies to a pull request when either condition is true:

- human acceptance or merge authorization is bound to an exact reviewed source head; or
- the PR uses a post-approval bounded-finalization phase.

Such a PR is a `covered PR` in this decision.

Routine pull requests whose governance does not bind approval to an exact commit are outside this decision unless a later policy brings them into scope.

## Definitions

- `reviewed head`: the exact commit SHA named in the human review or governance decision that grants acceptance or merge authorization.
- `final PR head`: the exact source-branch commit SHA selected for merge.
- `post-approval commit`: any source-branch commit added after the human decision bound to the reviewed head, regardless of whether its content is semantic, status-only, or governance-only.
- `bounded finalization`: an explicitly authorized post-approval change set restricted by a closed file and semantic allowlist and followed by recorded diff-scope validation.
- `compensating provenance`: the mandatory durable records required because squash merge does not preserve the source head as an ancestor of `main`.

## Proposed decision: Option A

### 1. Squash merge eligibility

A covered PR MAY use squash merge only when:

- the reviewed head and final PR head are the same exact commit;
- no post-approval commit exists;
- the human decision explicitly accepts that exact head and authorizes merge;
- the mandatory squash compensating-provenance package is complete before Issue closure; and
- no review finding, required change, or inconsistent human instruction remains open.

Equality is exact SHA equality. Equivalent trees, status-only differences, governance-only differences, and an agent's judgment that a later commit is harmless do not satisfy this rule.

### 2. Merge commit requirement

A covered PR MUST use a merge commit whenever the final PR head differs from the reviewed head because of any post-approval commit, including bounded finalization.

For that path:

- the final PR head MUST descend from the reviewed head;
- every intervening change MUST be within the human-authorized bounded-finalization scope;
- the exact `reviewed head..final PR head` diff and allowlist result MUST be recorded in PR or review metadata;
- any change outside the authorized scope voids the prior merge authorization and requires a new human review against a new exact head;
- the merge commit MUST retain the final PR head in `main` ancestry, thereby retaining the reviewed head as its ancestor.

A merge commit is not a substitute for human acceptance. It preserves topology after acceptance; it does not grant it.

### 3. Rebase-and-merge prohibition

Rebase-and-merge MUST NOT be used for a covered PR because it rewrites commit identities and prevents the exact reviewed source head from being the merged historical basis.

This proposal permits only:

- squash merge under the exact-head equality rule; or
- merge commit when a post-approval commit separates reviewed and final heads.

### 4. Mandatory compensating provenance for every squash

Every squash of a covered PR requires the complete package below, even when the reviewed and final heads are identical.

#### Before merge

The PR description MUST record:

- exact base branch and base SHA material to review;
- exact reviewed head;
- exact final PR head and the assertion that it equals the reviewed head;
- the human review or governance-decision artifact and outcome;
- unresolved finding disposition where applicable;
- explicit human merge authorization;
- the tracking Issue and applicable decision or milestone records;
- the statement that squash will sever source-head ancestry and therefore requires compensation.

A human-authored attestation comment or submitted review MUST:

- name the exact reviewed/final head;
- state the human's acceptance and merge authorization;
- state that acceptance and authorization were granted by the human, not inferred or supplied by the agent;
- contain no unresolved internal contradiction.

The agent MAY prepare an evidence package or suggested wording. The agent MUST NOT author, submit, reinterpret, repair, or infer the human attestation.

#### After merge and before tracking-Issue closure

A human-authored closure attestation on the PR or linked tracking Issue MUST:

- name the exact source head and actual squash merge SHA;
- state that the source head is not an ancestor of `main` after squash;
- identify the PR, review or governance decision, and project-memory records carrying compensating provenance;
- confirm that human acceptance and merge authorization preceded merge.

GitHub merge metadata is authoritative for the actual merge SHA. Repository content MUST NOT predict it.

The next governance-affecting project-memory PR MUST record the actual squash merge SHA when material, using the DEC-0004 self-provenance rule. Absence of an immediate recursive provenance PR is not a gap when the GitHub metadata and required human closure attestation already exist.

### 5. Provenance for merge-commit finalization

When a merge commit is required, the PR description or review record MUST retain:

- exact reviewed head;
- exact final PR head;
- exact bounded-finalization diff scope and validation result;
- the human decision authorizing bounded finalization and merge subject to successful validation;
- the actual merge commit after merge through GitHub metadata and later project-memory synchronization when material.

The separate post-merge squash closure attestation is not required solely for ancestry compensation because the reviewed and final heads remain in `main` ancestry. Any independent project rule requiring human closure still applies.

### 6. Human authority and inconsistent instructions

Only a human with applicable project authority may:

- accept the reviewed artifact;
- close review findings;
- authorize bounded finalization;
- authorize merge; or
- issue the required human attestations.

An agent MAY verify SHA equality, ancestry, file allowlists, and recorded metadata. Those checks do not confer acceptance or merge authority.

A verdict is void when it simultaneously grants approval or merge authorization and leaves a required finding, acceptance field, or governance gate open. The agent MUST NOT choose an interpretation or silently repair an inconsistent verdict; a human must reissue it.

### 7. Force-push and head movement

Any source-head movement after human review invalidates exact-head squash eligibility unless the final head returns to the same reviewed SHA. A rewritten, cherry-picked, or tree-equivalent commit is a different head and requires new human review or the authorized bounded-finalization merge-commit path, as applicable.

### 8. Effective boundary

This decision does not reopen, reverse, or reinterpret PR #26, REV-0013, Issue #20, or M1.2.5. They are historical evidence for the policy.

If accepted, this decision applies to REV-0014 and later covered reviews and governance decisions. Issue #28 remains a blocking gate until human decision and merge complete this Proposed record.

## Relationship to DEC-0004

This decision extends DEC-0004 and does not amend, supersede, or weaken it.

- DEC-0004 remains authoritative for repository-native project memory, Issue governance, update discipline, and self-provenance.
- DEC-0011 defines when covered PRs use squash or merge-commit topology and what squash compensation requires.
- DEC-0004's next-governance-update rule is one component of the DEC-0011 compensation package.

No text in DEC-0004 changes through this proposal.

## Bootstrap rule for this governance PR

This Proposed decision does not silently grant authority over its own merge.

- If the human governance decision is issued against the final PR head and no later commit occurs, squash is eligible only with the complete compensation package.
- If any acceptance, status, index, or other finalization commit follows the human decision, a merge commit is required.
- The Draft PR remains open until the human decision explicitly chooses an outcome and merge authorization.

## Rationale

Option A preserves a short squash history when one exact commit is both reviewed and merged. It requires topology-preserving merge commits precisely when review and finalization are distinct events. This makes the critical `reviewed head..final head` relationship reproducible from Git ancestry rather than only from mutable hosting metadata.

Mandatory compensation for every squash recognizes that even an equal reviewed/final source head is not an ancestor of `main` after squash. Human attestation and the DEC-0004 self-provenance rule retain authority and identity without pretending that a squash preserved topology.

## Alternatives considered

### Option B: squash by default for every covered PR

Not selected. A complete compensation package can preserve interpreted provenance, but it cannot make reviewed and finalization commits ancestors of `main`. Applying squash after bounded finalization would keep the critical diff-scope relationship dependent on external records.

### Merge commit for every covered PR

Not selected. When the exact reviewed head is also the final PR head, mandatory merge commits add topology without preserving an otherwise missing reviewed-to-finalization relationship. Squash with full compensation is sufficient for that case.

### Amend DEC-0004

Not selected. DEC-0004 governs the project-memory layer and its recording rules. Merge topology is independently decidable and should reference, not rewrite, that accepted foundation.

### Allow rebase-and-merge

Rejected because exact reviewed commit identities would be rewritten.

## Consequences

- Covered PRs have a deterministic merge-strategy rule.
- Bounded finalization after approval requires a merge commit.
- Squash remains available when human review is against the final exact head.
- Every covered squash requires explicit human and repository compensation.
- Agents can validate mechanics but cannot grant or infer acceptance.
- Some PRs will use merge commits despite the repository's prior squash preference.
- PR #29 must be updated to the governance PR's merged base and resolved-gate status before REV-0014, without semantic-contract enhancement.

## Related artifacts

- [Issue #28](https://github.com/ThresholdOps/MotiveForce/issues/28)
- [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20)
- [PR #26](https://github.com/ThresholdOps/MotiveForce/pull/26)
- [PR #29](https://github.com/ThresholdOps/MotiveForce/pull/29)
- [DEC-0004](DEC-0004-project-memory-governance.md), unchanged
- [OPEN_ITEMS.md](../OPEN_ITEMS.md)
- [CURRENT_STATE.md](../CURRENT_STATE.md)
- [SCOPE.md](../SCOPE.md)

## Supersedes

None.

## Superseded by

None.

## Follow-up actions

- Close Issue #28 after merge-commit and ancestry validation complete.
- Update PR #29 only for the new base and resolved governance-gate status; do not improve the M1.2.6 semantic contract before review.
- Do not start or freeze REV-0014 until PR #29 has that bounded synchronization.
- Record this PR's actual merge SHA in the next governance-affecting project-memory update when material; do not predict it here.
