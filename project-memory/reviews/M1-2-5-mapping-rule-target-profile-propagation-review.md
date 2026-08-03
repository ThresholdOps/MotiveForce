# REV-0011: M1.2.5 Mapping Rule and Target Profile Propagation Review

- Review ID: `REV-0011`
- Reviewed artifact: [docs/MAPPING_RULE_TARGET_PROFILE_PROPAGATION_CONTRACT.md](../../docs/MAPPING_RULE_TARGET_PROFILE_PROPAGATION_CONTRACT.md)
- Reviewed commit: [`1cb85a81b00bce4729bfc2ce58ad871ab67ee1d0`](https://github.com/ThresholdOps/MotiveForce/commit/1cb85a81b00bce4729bfc2ce58ad871ab67ee1d0)
- Review date: 2026-07-27T13:13:37Z
- Review type: Human semantic and design review
- Reviewer authority: Human project semantic and design review supplied with the correction instruction
- Review status: Completed
- Review outcome: Request changes
- Overall architecture: Retained
- Decision effect: No acceptance and no merge authorization
- Related PR: Draft [PR #26](https://github.com/ThresholdOps/MotiveForce/pull/26)
- Related Issue: [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20)
- Corrected successor: Requires human semantic and design re-review

## Summary

The Proposed M1.2.5 contract at `1cb85a81b00bce4729bfc2ce58ad871ab67ee1d0` received human semantic and design review.

The overall architecture is retained. Four bounded corrections are required: complete candidate coverage and unsuccessful-evaluation provenance, separation of ruleset capability requirements from executing compiler identity, an exact compatibility and transformation authority boundary, and replay-only use of `MAPPING_RULESET_UNRESOLVED`.

The corrected successor is not accepted by REV-0011 and requires human semantic and design re-review under REV-0012. Author self-review after correction is not human acceptance.

DEC-0009 remains `Proposed`. M1.2.5 remains `Proposed / In progress / not completed`.

## Findings

| Finding ID | Finding | Blocking reason | Required correction |
| --- | --- | --- | --- |
| `REV11-FIND-001` | Candidate coverage and unsuccessful-evaluation provenance are incomplete. | A request that applies no rule can lose the candidate-enumeration, filtering, prerequisite, and refusal basis needed for deterministic review and replay. | Require a conceptual `MappingEvaluationResult` for every request, complete ruleset candidate coverage, an exact enumeration/filter policy, explicit disposition or exact exclusion basis for every potentially applicable rule, unresolved treatment for omission, and preserved provenance when no application exists. |
| `REV11-FIND-002` | Ruleset policy identity and actual compiler capability identity are conflated. | Including the executing compiler build in ruleset identity would make implementation changes appear to mutate rule or ruleset policy identity. | Keep exact capability requirements or predicates in rule and ruleset identity; record the actual compiler implementation and capability realization in prerequisite evaluation, mapping evaluation, application, and replay bases. |
| `REV11-FIND-003` | Compatibility and transformation authority and proof boundaries are incomplete. | Agent proposals, model-specific Kernel validation, or a transformation record could otherwise be mistaken for authoritative general compatibility or proof of semantic preservation. | Define exact `ProfileCompatibilityAssessment` content and authority, restrict compiler derivation to Accepted deterministic policy, and require new mapping and compilation provenance when transformation changes semantics. |
| `REV11-FIND-004` | `MAPPING_RULESET_UNRESOLVED` is used for current compilation as well as replay. | The inherited code belongs to replay and verification; current mapping closure defects require existing compilation diagnostics. | Reserve `MAPPING_RULESET_UNRESOLVED` for replay and verification, and correct section 8.2, the crosswalk, example 22, and DEC-0009 summaries without adding a code. |

No additional blocking findings are supplied by REV-0011.

## Architecture retained

REV-0011 does not require redesign of:

- logical rule and immutable revision identity,
- exact ruleset closure and immutable versioning,
- the eight prerequisite categories and four prerequisite dispositions,
- the five candidate dispositions,
- deterministic selection among eligible semantically equivalent candidates,
- precedence and bounded fallback boundaries,
- exact target-profile identity,
- three directional compatibility outcomes,
- profile propagation,
- the 16-code inherited diagnostic crosswalk,
- Issue #8, Issue #9, and Issue #21 boundaries,
- the absence of implementation.

The conceptual provenance artifacts required by the findings do not create a runtime subsystem, schema, engine, registry, parser, validator, API, persistence model, test suite, or CI workflow.

## Review disposition

- Contract: remains `Proposed`.
- DEC-0009: remains `Proposed`.
- M1.2.5: remains `Proposed / In progress / not completed`.
- PR #26: remains Draft and unmerged.
- Issue #20: remains open and In progress.
- Acceptance: not granted.
- Merge authorization: not granted.
- Corrected successor: requires human semantic and design re-review under REV-0012.

## Remaining review questions

1. Are logical rule identity, immutable rule revision, and exact ruleset closure correctly separated?
2. Are rule prerequisites and prerequisite-satisfaction semantics sufficiently complete?
3. Is `MappingRuleApplication` correctly separated from agent proposals, rule definitions, and Kernel validation?
4. Are multi-rule applicability, precedence, fallback, and equivalent-representation rules safely bounded?
5. Are exact target-profile identity, directional compatibility, and explicit transformation semantics correct?
6. Is target-profile propagation across compiler, replay, and Kernel artifacts complete?
7. Are authority, diagnostic, Issue #9, partial-compilation, and replay boundaries clean?
8. Is the Proposed M1.2.5 design ready for acceptance?
