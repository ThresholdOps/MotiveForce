# Current State

- Last verified: 2026-08-03T10:42:06Z
- Verification source: fetched GitHub `main` at [`2387307f2f7a3f05b65197497b9f0945bb26bf6a`](https://github.com/ThresholdOps/MotiveForce/commit/2387307f2f7a3f05b65197497b9f0945bb26bf6a); PR #30 exact reviewed head [`e0020a44b0b649b711402d282d4cf5ece31708a8`](https://github.com/ThresholdOps/MotiveForce/commit/e0020a44b0b649b711402d282d4cf5ece31708a8) and [human governance decision](https://github.com/ThresholdOps/MotiveForce/pull/30#issuecomment-5165269810); Issue #28; ID registries on `main`, active PR #29, and the DEC-0011 governance branch.
- Governance finalization and merge provenance for PR #30 are retained in PR and Issue metadata; repository content does not predict its own finalization or merge SHA.

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
- REV-0014 does not exist as a review record and MUST NOT begin until PR #29 has been synchronized only to the new `main` base and resolved governance-gate status.

## Completed governance work

- [Issue #28](https://github.com/ThresholdOps/MotiveForce/issues/28), `OPEN-0021`, is completed through merge of PR #30 and closes after merge validation.
- [DEC-0011](decisions/DEC-0011-reviewed-finalization-merge-strategy.md) is Accepted through merge of PR #30. The project owner approved Option A at exact reviewed head `e0020a44b0b649b711402d282d4cf5ece31708a8`, with no findings.
- Every covered squash requires the complete compensating-provenance package defined by DEC-0011.
- DEC-0011 extends but does not amend or supersede DEC-0004.
- The governance finalization does not change PR #29 or the M1.2.6 semantic contract.

## ID allocation across active branches

- PR #29 already allocates `DEC-0010`, `OPEN-0020`, `HIST-0045`, `HIST-0046`, `CHG-0033`, and `CHG-0034`.
- The governance work allocates `DEC-0011`, reuses the already registered `OPEN-0021`, and allocates `HIST-0047`, `HIST-0048`, `CHG-0035`, and `CHG-0036`.
- IDs are not reused merely because the allocating PR has not merged.

## Current gates

- The Issue #28 merge-strategy gate is resolved through human acceptance and merge of PR #30.
- PR #29 must be updated only to the new base and resolved-gate status, without pre-review semantic enhancement.
- REV-0014 remains unstarted until that bounded PR #29 synchronization is complete.

## Next expected action

Synchronize PR #29 only to the new `main` base and resolved Issue #28 gate, record PR #30's actual merge SHA under the DEC-0004 self-provenance rule, and do not improve the M1.2.6 semantic contract before REV-0014.

## Out of scope

- any change to the M1.2.6 semantic contract;
- REV-0014 or its evidence package;
- schema, fixture, prompt, training, implementation, validator, test, or CI;
- branch-protection or GitHub automation implementation;
- reopening or reinterpreting PR #26, Issue #20, REV-0013, or M1.2.5;
- amending or superseding DEC-0004.
