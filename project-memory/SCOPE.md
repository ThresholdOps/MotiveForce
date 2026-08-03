# Scope

## Current product scope

Current product scope remains conceptual and pre-MVP:

- semantic analysis of process sources;
- evidence-backed canonical semantic model;
- explicit uncertainty and contradiction handling;
- Process IR boundary between Analytical Agent and Semantic Compiler;
- future deterministic BPMN 2.0.2 compilation and validation;
- future export projections.

## Completed scope

- M1 Process IR contract and M1.1 project-memory governance are accepted.
- M1.2.1 through M1.2.5 design-contract work is accepted and completed.
- PR #26 is squash-merged at [`2387307f2f7a3f05b65197497b9f0945bb26bf6a`](https://github.com/ThresholdOps/MotiveForce/commit/2387307f2f7a3f05b65197497b9f0945bb26bf6a); Issue #20 is closed after human attestation.

## Concurrent but separated current work

### M1.2.6 semantic design

[Issue #27](https://github.com/ThresholdOps/MotiveForce/issues/27) and Draft [PR #29](https://github.com/ThresholdOps/MotiveForce/pull/29) contain the Proposed M1.2.6 structured-elicitation contract and `DEC-0010`.

This standalone governance work does not contain or modify that contract. REV-0014 remains unstarted until PR #29 is synchronized only to the new `main` base and resolved Issue #28 gate.

### Merge-strategy governance

[Issue #28](https://github.com/ThresholdOps/MotiveForce/issues/28), `OPEN-0021`, is completed through merge of PR #30.

[DEC-0011](decisions/DEC-0011-reviewed-finalization-merge-strategy.md) accepts Option A:

- squash merge is eligible only when the exact reviewed head equals the final PR head and no post-approval commit exists;
- merge commit is required whenever bounded finalization or another authorized post-approval commit separates the reviewed and final heads;
- rebase-and-merge is prohibited for covered PRs;
- every covered squash requires explicit compensating provenance and human attestation;
- human acceptance and merge authorization cannot be inferred by an agent;
- DEC-0011 extends DEC-0004 without amendment or supersession.

## Governance acceptance boundary

The project owner personally reviewed exact head [`e0020a44b0b649b711402d282d4cf5ece31708a8`](https://github.com/ThresholdOps/MotiveForce/commit/e0020a44b0b649b711402d282d4cf5ece31708a8), approved Option A with no findings, authorized the bounded finalization allowlist, and authorized merge after successful diff-scope validation in the [human governance decision](https://github.com/ThresholdOps/MotiveForce/pull/30#issuecomment-5165269810). Acceptance is granted by the human and completed through merge of PR #30, not inferred by the agent.

## Explicit non-goals

- no M1.2.6 semantic-contract change;
- no REV-0014;
- no schema, fixture, evaluation, test, CI, prompt, training, or implementation;
- no GitHub automation or branch-protection implementation;
- no retrospective change to PR #26 or M1.2.5;
- no DEC-0004 amendment or supersession;
- no normative DEC-0011 change during bounded finalization.

## Future transition

After DEC-0011 is accepted and its governance PR merges, PR #29 may be updated only for:

- the new `main` base;
- the resolved Issue #28 gate;
- required project-memory conflict resolution and status synchronization.

That update must not improve or otherwise change the M1.2.6 semantic contract before REV-0014.
