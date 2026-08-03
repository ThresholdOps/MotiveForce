# Current State

- Last verified: 2026-08-03T10:24:04Z
- Verification source: fetched GitHub `main` and direct remote-head query at [`2387307f2f7a3f05b65197497b9f0945bb26bf6a`](https://github.com/ThresholdOps/MotiveForce/commit/2387307f2f7a3f05b65197497b9f0945bb26bf6a); all open PRs and open/closed Issues; ID registries on `main` and active PR #29 head [`49b12d2133a804ce350568cf487556ec057f0f6c`](https://github.com/ThresholdOps/MotiveForce/commit/49b12d2133a804ce350568cf487556ec057f0f6c).
- Active governance branch: `agent/merge-strategy-governance`, based exactly on `2387307f2f7a3f05b65197497b9f0945bb26bf6a`.

## Project status

MøtiveFōrce is `Concept / pre-MVP`.

No application, runtime agent, Semantic Compiler, BPMN Kernel, validator, user interface, export adapter, schema, fixture, or executable test suite is implemented in merged repository content.

## Architecture thesis

The canonical semantic model is the source of truth. The Analytical Agent interprets source material without accepting business meaning or validating BPMN. The Semantic Compiler maps accepted meaning. The BPMN Kernel validates the resulting BPMN model.

## Completed design work

- M0, M1, and M1.1 are completed through PRs #1-#3.
- M1.2.1 through M1.2.4 are accepted and completed through PRs #22-#25.
- M1.2.5 is accepted and completed through squash merge of [PR #26](https://github.com/ThresholdOps/MotiveForce/pull/26) at [`2387307f2f7a3f05b65197497b9f0945bb26bf6a`](https://github.com/ThresholdOps/MotiveForce/commit/2387307f2f7a3f05b65197497b9f0945bb26bf6a). [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20) is closed after the project owner's human attestation.

## Active semantic-design work

- [Issue #27](https://github.com/ThresholdOps/MotiveForce/issues/27), `OPEN-0020`, tracks M1.2.6 structured elicitation extraction.
- Draft [PR #29](https://github.com/ThresholdOps/MotiveForce/pull/29) is the only active semantic-design PR. Its exact head is `49b12d2133a804ce350568cf487556ec057f0f6c` and its base is `2387307f2f7a3f05b65197497b9f0945bb26bf6a`.
- `DEC-0010` and M1.2.6 are Proposed in PR #29. They are not duplicated by this governance branch.
- REV-0014 does not exist as a review record and MUST NOT begin while Issue #28 remains unresolved.

## Active governance work

- [Issue #28](https://github.com/ThresholdOps/MotiveForce/issues/28), `OPEN-0021`, is consciously started as a separate governance item.
- [DEC-0011](decisions/DEC-0011-reviewed-finalization-merge-strategy.md) is Proposed and selects Option A for human decision: squash only when the exact reviewed head equals the final PR head; merge commit when a post-approval commit separates them.
- Every covered squash would require the complete compensating-provenance package defined by DEC-0011.
- DEC-0011 extends but does not amend or supersede DEC-0004.
- The governance proposal does not change PR #29 or the M1.2.6 semantic contract.

## ID allocation across active branches

- PR #29 already allocates `DEC-0010`, `OPEN-0020`, `HIST-0045`, `HIST-0046`, `CHG-0033`, and `CHG-0034`.
- This governance branch allocates `DEC-0011`, reuses the already registered `OPEN-0021`, and allocates `HIST-0047` and `CHG-0035`.
- IDs are not reused merely because the allocating PR has not merged.

## Current gates

- DEC-0011 requires a separate human governance decision before acceptance or merge.
- Issue #28 remains blocking for REV-0014 until the governance decision is accepted and merged.
- After governance merge, PR #29 must be updated only to the new base and resolved-gate status, without pre-review semantic enhancement.

## Next expected action

Review the standalone DEC-0011 Draft PR. Do not start REV-0014 and do not merge the governance PR without an explicit human governance decision against an exact source head.

## Out of scope

- any change to the M1.2.6 semantic contract;
- REV-0014 or its evidence package;
- schema, fixture, prompt, training, implementation, validator, test, or CI;
- branch-protection or GitHub automation implementation;
- reopening or reinterpreting PR #26, Issue #20, REV-0013, or M1.2.5;
- amending or superseding DEC-0004.
