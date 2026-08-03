# REV-0013: M1.2.5 Mapping Rule and Target Profile Propagation Final Re-Review

- Review ID: `REV-0013`
- Review date: 2026-08-03T08:39:36Z
- Reviewer role: Human project semantic and design approver, informed by an independent AI semantic and architectural review
- Repository: [ThresholdOps/MotiveForce](https://github.com/ThresholdOps/MotiveForce)
- Reviewed artifact: [docs/MAPPING_RULE_TARGET_PROFILE_PROPAGATION_CONTRACT.md](../../docs/MAPPING_RULE_TARGET_PROFILE_PROPAGATION_CONTRACT.md)
- Reviewed semantic head: [`f8d2249e4693305b57bf021c76bdd78b010da24b`](https://github.com/ThresholdOps/MotiveForce/commit/f8d2249e4693305b57bf021c76bdd78b010da24b)
- Base commit: [`20f53f13938692b9c572b6f9f963e89fc22cb5b8`](https://github.com/ThresholdOps/MotiveForce/commit/20f53f13938692b9c572b6f9f963e89fc22cb5b8)
- Prior reviewed semantic head: [`7a6ec176a0fcc738a5c56a9c98a7d946446a2c01`](https://github.com/ThresholdOps/MotiveForce/commit/7a6ec176a0fcc738a5c56a9c98a7d946446a2c01)
- Prior review: [REV-0012](M1-2-5-mapping-rule-target-profile-propagation-review-2.md)
- Related PR: Draft [PR #26](https://github.com/ThresholdOps/MotiveForce/pull/26)
- Related Issue: [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20)
- Review type: Human semantic and design final re-review
- Review status: Completed
- Human acceptance date: 2026-08-03T08:50:59Z
- Review outcome: Approve
- Decision effect: Both REV-0012 findings are closed; the contract, DEC-0009, and all 15 design choices are approved; M1.2.5 is approved for completion through merge of PR #26
- Human acceptance effect: Granted by the explicit finalization instruction after review of the independent evidence and verdict
- Merge effect: Authorized after bounded-finalization diff-scope validation; this record does not perform the merge
- Implementation effect: None; implementation remains not started

## 1. Review authority and frozen boundary

This review evaluates the complete Proposed M1.2.5 semantic design at exact commit `f8d2249e4693305b57bf021c76bdd78b010da24b`. That commit is the final semantic head for REV-0013. The contract, DEC-0009, prior reviews, nine-scenario evidence package, accepted M1 through M1.2.4 contracts, the nine previously uncovered diagnostic anchors, and section 26.1 were read as one review basis.

This record memorializes the human semantic and design approval supplied after the independent AI review verdict. Human approval adopts the `Approve` outcome, closes both REV-0012 findings, accepts the 15 design choices including every Potential semantic change, approves the contract and DEC-0009 for repository-authoritative acceptance through merge of PR #26, and authorizes bounded finalization and merge after validation. It does not perform the merge, authorize implementation, or close Issue #20 before merge.

The review excludes schemas, registries, compiler or Kernel implementation, executable validation, APIs, persistence, CI, Issue #8 dependency-closure implementation, Issue #9 metamodel and conformance strategy, and Issue #21 contract fixtures.

## 2. Evidence inspected

- Complete Proposed [M1.2.5 contract](../../docs/MAPPING_RULE_TARGET_PROFILE_PROPAGATION_CONTRACT.md) at the reviewed semantic head.
- Proposed [DEC-0009](../decisions/DEC-0009-mapping-rule-target-profile-propagation.md) at the reviewed semantic head.
- [REV-0011](M1-2-5-mapping-rule-target-profile-propagation-review.md) and [REV-0012](M1-2-5-mapping-rule-target-profile-propagation-review-2.md).
- Exact semantic correction range `7a6ec176a0fcc738a5c56a9c98a7d946446a2c01..f8d2249e4693305b57bf021c76bdd78b010da24b` and reviewer-attention correction range `bcf6b150fed303c03e1c685eb1462eccd4703c1f..f8d2249e4693305b57bf021c76bdd78b010da24b`.
- Accepted [M1 Process IR contract](../../docs/PROCESS_IR_CONTRACT.md), [M1.2.1 RecordEnvelope contract](../../docs/PROCESS_IR_RECORD_ENVELOPE_CONTRACT.md), [M1.2.2 replay contract](../../docs/SEMANTIC_COMPILER_REPLAY_CONTRACT.md), [M1.2.3 diagnostic policy](../../docs/PROCESS_IR_DIAGNOSTIC_POLICY_CONTRACT.md), and [M1.2.4 AnalystDecision staleness contract](../../docs/ANALYST_DECISION_STALENESS_REVALIDATION_CONTRACT.md).
- The existing non-authoritative REV-0013 evidence package containing `REV13-SCN-01` through `REV13-SCN-09`; the package was not regenerated.
- The eight human-review questions in PR #26 and contract section 25.
- The nine direct contract anchors supplied for aspects not isolated as evidence-package scenarios.
- The three reviewer-attention clarifications in contract section 26.1.
- Draft PR #26 head and status and open Issue #20 status.

No runtime behavior is asserted by this review. The evidence basis is contract text at the frozen semantic head.

## 3. Evidence-package quotation verification

The existing evidence package remains historically anchored to `bcf6b150fed303c03e1c685eb1462eccd4703c1f`. It was not regenerated or rewritten. During REV-0013, every quoted normative sentence was checked for exact word-for-word presence at `f8d2249e4693305b57bf021c76bdd78b010da24b`; only its current line location was re-established.

| Evidence scenario | Quotation result at `f8d2249` | Current contract line |
| --- | --- | --- |
| `REV13-SCN-01` | Exact verbatim match | 309 |
| `REV13-SCN-02` | Exact verbatim match | 470 |
| `REV13-SCN-03` | Exact verbatim match | 440 |
| `REV13-SCN-04` | Exact verbatim match | 441 |
| `REV13-SCN-05` | Exact verbatim match | 260 |
| `REV13-SCN-06` | Exact verbatim match | 891 |
| `REV13-SCN-07` | Exact verbatim match | 261 |
| `REV13-SCN-08` | Exact verbatim match | 938 |
| `REV13-SCN-08` additional partial-result quotation | Exact verbatim match | 940 |
| `REV13-SCN-09` | Exact verbatim match | 779 |

The old line links in the evidence package are therefore stale locators, not stale quotations or changed evidence meaning.

## 4. Nine-scenario review

| Scenario | Final assessment | Review basis |
| --- | --- | --- |
| `REV13-SCN-01` - changed enumeration policy | Satisfied | Sections 8.3-8.4 and 20 require a new ruleset revision and changed semantic and replay basis even when candidates and outputs remain equal. |
| `REV13-SCN-02` - omitted expected candidate | Satisfied | Sections 10.1, 10.3, 21, and 21.2 make omission unresolved, assign `PROVENANCE_MISSING`, and forbid a clean exclusion, ineligibility, or application. |
| `REV13-SCN-03` - unrealized compiler capability | Satisfied | Sections 10.2, 21, and 21.3 assign `UNSUPPORTED_MAPPING` after valid closure and exclude `MAPPING_NOT_ELIGIBLE`. |
| `REV13-SCN-04` - non-capability eligibility failure | Satisfied | Sections 10.2, 21, and 21.3 assign `MAPPING_NOT_ELIGIBLE` unless a more specific inherited diagnostic owns the exact condition. |
| `REV13-SCN-05` - malformed or cyclic active closure | Satisfied | Sections 8.2 and 21.1 assign `UNRESOLVED_REFERENCE` before candidate and capability evaluation. |
| `REV13-SCN-06` - unreconstructable historical ruleset closure | Satisfied | Sections 20 and 21 reserve `MAPPING_RULESET_UNRESOLVED` for replay or verification and make the affected scope `not replayable`. |
| `REV13-SCN-07` - missing or contradictory governing policy | Satisfied | Sections 8.2, 21, and 21.3 assign `MODELING_POLICY_REQUIRED` after exact references resolve and preserve more-specific representation-policy diagnostics. |
| `REV13-SCN-08` - partial compilation | Satisfied | Section 21.2 forbids unresolved request output from reaching the Kernel and requires failed-request, universe, diagnostic, scope, and policy provenance in the partial result. |
| `REV13-SCN-09` - Kernel-facing provenance | Satisfied | Sections 16-18 require a closed, resolvable chain through universe, evaluation, application, compiled outputs, replay manifest, and Kernel-facing provenance without Kernel re-enumeration. |

All nine textual assessments remain satisfied at the frozen semantic head. This verifies the selected scenarios but is not, by itself, the basis for closing either finding; finding closure also depends on the direct review below.

## 5. Direct review of aspects outside the nine-scenario package

| Previously unisolated aspect | Frozen-head anchor and conclusion |
| --- | --- |
| Historical manifest lacks policy identity or frozen parameters | Sections 20, 21, and 21.3 and `SCN-C15` assign sole primary ownership to `REPLAY_POLICY_UNRESOLVED`. |
| Exact historical policy identity exists but cannot resolve | Sections 20 and 21 and `SCN-C09` assign `REPLAY_DEPENDENCY_UNRESOLVED`. |
| Historical policy uses a mutable selector | Sections 20 and 21 assign only `FLOATING_REPLAY_DEPENDENCY`; `SCN-C09` preserves the distinction. |
| Current basis uses a mutable selector | Sections 8.2, 10.1, and 21 and Example 2 assign `FLOATING_EXTERNAL_BASIS` before resolution. |
| Replay diagnostic separation | Section 20 and the normative matrix distinguish missing policy identity, unresolved exact dependency, mutable dependency, unreconstructable ruleset closure, absent non-policy input or universe evidence, and changed available basis. |
| Exact unresolved current import without a cycle | Sections 8.2 and 21 and Example 22 assign `UNRESOLVED_REFERENCE`; replay reconstruction remains separate. |
| Simultaneous closure defect and apparent capability defect | Section 21.1 and `SCN-C12` give closure precedence and forbid speculative `UNSUPPORTED_MAPPING`. |
| Historical candidate-universe evidence is absent | Sections 20, 21, and 21.3 assign `REPLAY_INPUT_CLOSURE_INCOMPLETE` only after exact policy identity and frozen parameters are present. |
| Specific representation-policy diagnostic versus generic modeling policy | The diagnostic matrix and section 21.3 preserve the three specific representation-policy diagnostics and their precedence over `MODELING_POLICY_REQUIRED`. |

These anchors close the coverage gap identified by the evidence package's reverse mapping without expanding or regenerating that package.

## 6. Section 26.1 reviewer-attention conclusions

### Imported enumeration-policy authority

Approved by this review. The request-selected ruleset's directly owned policy is the sole operative enumeration policy across the complete imported closure. Imported policies remain immutable transitive identity and replay provenance, are inert for the importing request, and differ without creating conflict unless more than one policy is claimed as operative. Revision cascade and path-dependent operativeness are explicit.

### Current candidate-source failure ownership

Approved by this review. Mutable selector, unresolved exact reference, unrealized compiler capability, absent authoritative universe provenance after completed deterministic assessment, and interrupted execution are phase-distinct. `UNRESOLVED_REFERENCE` retains its accepted narrow meaning. `PROVENANCE_MISSING` owns inability to establish required candidate-universe provenance after a completed assessment. An interrupted assessment remains an execution failure and produces no inferred semantic mapping diagnostic.

### Missing replay-policy precedence

Approved by this review. `REPLAY_POLICY_UNRESOLVED` is the sole primary diagnostic for absent policy identity or incomplete frozen parameters. `REPLAY_INPUT_CLOSURE_INCOMPLETE` is limited to missing non-policy inputs and candidate-universe evidence after the exact policy basis is present. The exclusion is mutual and phase precedence is explicit.

No new finding arises from section 26.1.

## 7. Eight review questions

| ID | Answer | Basis |
| --- | --- | --- |
| `RQ-01` | Yes. | Logical rule identity, immutable rule revision, exact ruleset revision, imports, request-selected operative policy, inert imported-policy provenance, and compiler identity are separated. |
| `RQ-02` | Yes. | Eight prerequisite categories, four explicit dispositions, exact satisfaction records, omission behavior, and business-versus-modeling-policy authority are complete at this design boundary. |
| `RQ-03` | Yes. | `MappingRuleApplication` is compiler-owned, references exact evaluation and universe records, exists only for an applied rule, and is distinct from Agent proposals, definitions, decisions, compatibility assessments, and Kernel reports. |
| `RQ-04` | Yes. | Selection and precedence are limited to eligible semantically equivalent candidates; conflict, missing prerequisites, unsupported meaning, and lossy fallback remain blocking. |
| `RQ-05` | Yes. | Profile identity is exact; compatibility is directional, scoped, version-specific, and authorized; transformation is explicit, immutable, replay-affecting, and not semantic proof by itself. |
| `RQ-06` | Yes. | Exact profile and candidate-enumeration provenance propagate through request, evaluation, application, compiled artifacts, replay manifest, verification evidence, and Kernel-facing provenance. |
| `RQ-07` | Yes. | Agent, Compiler, and Kernel authority remain separate; diagnostics have phase and precedence ownership; replay and current compilation remain distinct; Issue #8, Issue #9, and Issue #21 retain their deferred implementation scopes. |
| `RQ-08` | Yes. | The two blocking REV-0012 defects are resolved, the three reviewer-attention clarifications are coherent, no new blocking semantic defect was found, and human semantic and design approval was supplied. |

## 8. Finding disposition

| Finding ID | Final review disposition | Basis |
| --- | --- | --- |
| `REV12-FIND-001` | Closed | Candidate-enumeration policy is an exact ruleset-closure member; the request-selected ruleset owns one operative policy across imports; policy change creates a new ruleset and changed replay basis; `CandidateUniverseRecord` closes coverage; exact provenance reaches replay, partial outputs, and Kernel-facing artifacts. |
| `REV12-FIND-002` | Closed | The normative matrix and phase precedence create a non-overlapping primary-code partition for active closure, provenance, capability, eligibility, modeling policy, profile, replay dependency, replay policy, replay input closure, and changed-basis conditions while preserving inherited meanings. |

No new finding is created by REV-0013.

## 9. Design-choice assessment

`MAP-CHOICE-001` through `MAP-CHOICE-015` are Accepted by human semantic and design review. The seven choices classified as Potential semantic changes are explicitly accepted within their bounded definitions, authority limits, provenance requirements, diagnostics, and tests.

## 10. Bounded-finalization diff-scope governance

The reviewed semantic head remains `f8d2249e4693305b57bf021c76bdd78b010da24b`. Before merge, validation MUST prove that `git diff f8d2249e4693305b57bf021c76bdd78b010da24b..final-head` touches only this review record and its review index; status-only, finding-disposition, acceptance-effect, and completion metadata in the contract, DEC-0009, M1.2.5 milestone, parent milestone, `CURRENT_STATE.md`, `OPEN_ITEMS.md`, `HISTORY.md`, `CHANGELOG.md`, directly affected project-memory indexes, and PR or Issue provenance needed for bounded finalization and merge preparation. The diff MUST contain no new or modified normative semantic rule, definition, invariant, diagnostic trigger or precedence, example, test expectation, authority boundary, or Issue boundary. A change outside this allowlist, or any normative change inside an allowed file, invalidates this approval verdict; the agent MUST stop finalization and require a new semantic review rather than infer that the change is harmless.

## 11. Final review outcome

`Approve`

The final semantic head resolves both REV-0012 findings without redesigning adjacent layers, changing the accepted diagnostic inventory, or crossing implementation boundaries. Exact identity, candidate coverage, deterministic diagnostic ownership, target-profile propagation, replay, partial-compilation visibility, and Kernel authority form one coherent Proposed design.

The contract and DEC-0009 are approved for repository-authoritative acceptance through merge of PR #26. Bounded finalization is authorized under the diff-scope invariant above.

## 12. Explicit status

| Status | Value |
| --- | --- |
| REV-0013 completed | Yes |
| REV-0013 outcome | Approve |
| `REV12-FIND-001` | Closed by REV-0013; human disposition adopted |
| `REV12-FIND-002` | Closed by REV-0013; human disposition adopted |
| New REV-0013 findings | None |
| Human acceptance performed | Yes |
| Contract status | Accepted; repository-authoritative through merge of PR #26 |
| DEC-0009 status | Accepted; repository-authoritative through merge of PR #26 |
| M1.2.5 completed | Approved for completion through merge of PR #26 |
| PR #26 Draft | Yes |
| PR #26 merged | No |
| Issue #20 closed | No |
| Merge authorization | Yes, after bounded-finalization validation |
| Implementation authorization | No |

## 13. Provenance qualification

The complete Proposed M1.2.5 contract and DEC-0009 at `f8d2249e4693305b57bf021c76bdd78b010da24b` were reviewed against the accepted basis, prior findings, all eight review questions, all nine evidence-package scenarios, every quotation carried by that package, the direct anchors for its previously uncovered aspects, and section 26.1. The evidence package was not regenerated; its quotations were reverified against the frozen head and re-anchored only in this review record.

This record combines the independent AI semantic and architectural evidence and `Approve` verdict with the subsequent explicit human semantic and design acceptance. Merge is authorized after bounded-finalization validation; implementation remains unauthorized.
