# M1 Process IR Semantic Review

- Review ID: `REV-0001`
- Reviewed artifact: `docs/PROCESS_IR_CONTRACT.md` in Draft [PR #2](https://github.com/ThresholdOps/MotiveForce/pull/2)
- Review status: Completed

## Author self-check

- Reviewed commit: [`34d2ccfa752ef10742ccf2e81f0e09757c11a240`](https://github.com/ThresholdOps/MotiveForce/commit/34d2ccfa752ef10742ccf2e81f0e09757c11a240)
- Date: 2026-07-22T19:47:04Z
- Reviewer authority: author self-check only
- Outcome: Structural self-check passed according to PR #2 body, but semantic acceptance was not claimed.

## First human semantic review

- Review date: Unverified from GitHub review object; review findings are evidenced by PR #2 body after correction.
- Reviewer authority: Human semantic review, as recorded in PR #2 body.
- Reviewed commit: [`34d2ccfa752ef10742ccf2e81f0e09757c11a240`](https://github.com/ThresholdOps/MotiveForce/commit/34d2ccfa752ef10742ccf2e81f0e09757c11a240)

## Findings and requested corrections

| Finding | Blocking status | Requested correction |
| --- | --- | --- |
| `RecommendedDecision` missing from package envelope. | Blocking for contract completeness. | Add `recommended_decisions`. |
| Confidence could influence recommendations too strongly. | Blocking for authority model. | Prohibit confidence-only recommendations and add `no-recommendation`. |
| Single value-state model mixed epistemic state, applicability, requirement, and absence. | Blocking for semantics. | Replace with four independent dimensions and validity constraints. |
| Package direction and compiler output were unclear. | Blocking for boundary clarity. | Separate `ProcessIRPackage`, `CompilationResult`, and downstream validation report. |
| Proposed records could be read as authoritative compiler input. | Blocking for authority. | Define proposed-record inspection boundary. |
| Mapping eligibility authority was unclear. | Blocking for compiler boundary. | Assign eligibility to Semantic Compiler. |
| `AnalystDecision` could substitute for evidence. | Blocking for evidence model. | Require evidence for accepted source-derived assertions. |
| `ModelingDecision` placement was ambiguous. | Blocking for governance. | Place explicitly. |

## First corrected commit

- Corrected commit: [`f32543d778af2dbbdf1d5f48565cf3e141819f67`](https://github.com/ThresholdOps/MotiveForce/commit/f32543d778af2dbbdf1d5f48565cf3e141819f67)
- Correction status: Applied in Draft PR #2; later superseded by focused corrections.

## Second human semantic review

- Review date: Unverified from GitHub review object; review findings are evidenced by PR #2 body after focused correction.
- Reviewer authority: Human semantic review, as recorded in PR #2 body.
- Reviewed commit: [`f32543d778af2dbbdf1d5f48565cf3e141819f67`](https://github.com/ThresholdOps/MotiveForce/commit/f32543d778af2dbbdf1d5f48565cf3e141819f67)

## Focused requested corrections

| Finding | Blocking status | Requested correction |
| --- | --- | --- |
| Explicitly known absence was too restricted. | Blocking for value semantics. | Support evidence-backed known absence without confusing it with unknown or not-applicable. |
| `ModelingDecision` appeared in insufficient-evidence remediation. | Blocking for evidence authority. | Remove modeling decisions as remediation for insufficient business evidence. |
| Semantic compilation policy included presentation concerns. | Blocking for component boundary. | Restrict `CompilationPolicyContext` and identify downstream rendering policy separately. |
| Unknown interpretation could be treated as ambiguity. | Blocking for diagnostics. | Add `UNRESOLVED_INTERPRETATION` and distinguish it from ambiguity. |

## Focused corrected commit

- Corrected commit: [`96c2d1ee50f876a8fd0d895b72770e0faf92427c`](https://github.com/ThresholdOps/MotiveForce/commit/96c2d1ee50f876a8fd0d895b72770e0faf92427c)
- Correction status: Applied in Draft PR #2; later superseded by final hardening.

## Final M1 semantic-hardening review

- Review date: Unverified from GitHub review object; review findings are evidenced by PR #2 body after final hardening.
- Reviewer authority: Human semantic review, as recorded in PR #2 body.
- Reviewed commit: [`96c2d1ee50f876a8fd0d895b72770e0faf92427c`](https://github.com/ThresholdOps/MotiveForce/commit/96c2d1ee50f876a8fd0d895b72770e0faf92427c)

## Final hardening requested corrections

| Finding | Blocking status | Requested correction |
| --- | --- | --- |
| Semantic context was implicit. | Blocking for contextual authority. | Add `SemanticContext` and `context_ref` rules. |
| Human decision authority semantics were not explicit enough. | Blocking for M1 authority. | Add `DecisionAuthorityRef` and require it for authoritative `AnalystDecision` records. |
| Compiler output artifact was under-specified. | Blocking for pipeline boundary. | Add `CompiledSemanticModel` separate from `CompilationResult`. |
| Business-semantic and modeling-policy diagnostics could overlap. | Blocking for remediation discipline. | Split business and modeling diagnostics. |
| Partial compilation existed without explicit policy. | Blocking for compilation outcome clarity. | Disable partial compilation by default and require explicit policy to enable it. |
| Analyst decisions assumed interpretation selection. | Blocking for decision semantics. | Add `AnalystDecision.decision_outcome`. |
| BPMN validity was not profile-scoped enough. | Blocking for conformance claims. | Add `target_bpmn_profile` propagation. |
| Required versus not-applicable wording could be misread. | Blocking for value-state semantics. | Correct requirement evaluation rules. |

## Final hardening corrected commit

- Corrected commit: [`59f1cde14c118bc8f0dcc0e1d6ebc2784a2ec600`](https://github.com/ThresholdOps/MotiveForce/commit/59f1cde14c118bc8f0dcc0e1d6ebc2784a2ec600)
- Correction status: Applied in Draft PR #2; later superseded by final normative corrections.

## Final normative corrections and acceptance provenance

- Reviewed artifact: `docs/PROCESS_IR_CONTRACT.md`
- Fully reviewed predecessor commit: [`59f1cde14c118bc8f0dcc0e1d6ebc2784a2ec600`](https://github.com/ThresholdOps/MotiveForce/commit/59f1cde14c118bc8f0dcc0e1d6ebc2784a2ec600)
- Final correction set: explicitly approved without independent full re-read
- Final amended source head: [`b2d6fe8f2192149145e04cbf2f0e5ffea737e1c0`](https://github.com/ThresholdOps/MotiveForce/commit/b2d6fe8f2192149145e04cbf2f0e5ffea737e1c0)
- Squash merge commit: [`54d5e814601788574d13761561867ce5982cc88c`](https://github.com/ThresholdOps/MotiveForce/commit/54d5e814601788574d13761561867ce5982cc88c)
- Post-merge check performed: structural, diff-match against the approved correction set
- Post-merge check NOT performed: independent semantic re-review of the merged text
- Review outcome: Conditional human acceptance. Acceptance rests on full review of the predecessor plus explicit approval of the stated correction set, confirmed structurally intact after merge. This is not equivalent to a full semantic read of the final artifact.
- Provenance qualification: Full predecessor review plus explicit correction-set approval plus post-merge structural confirmation.

| Finding | Blocking status | Correction |
| --- | --- | --- |
| Duplicate ambiguity compiler diagnostics remained. | Blocking for diagnostic clarity. | Consolidated compiler ambiguity into `AMBIGUOUS_BUSINESS_MEANING`. |
| Refusal wording could be read globally despite partial compilation. | Blocking for partial-compilation consistency. | Made refusal scope-local for every affected requested scope or fragment. |
| Event-trigger remediation allowed mapping bypass. | Blocking for business-semantics authority. | Required trigger evidence, authorized decision, exclusion, or deferral; mapping choices cannot bypass unresolved event semantics. |
| Final list punctuation was inconsistent. | Non-blocking editorial defect. | Corrected punctuation in the “not open in M1” list. |

## Final review outcome

Completed with conditional human acceptance. PR #2 was squash-merged, and the M1 Process IR contract remains `Accepted` for the conceptual M1 scope. The acceptance basis is the full review of `59f1cde...`, explicit approval of the bounded final correction set, and structural confirmation that the approved corrections were present in `b2d6fe8...` after merge with no architecture drift detected in those corrections.

This qualification corrects the review record. It does not reopen or reverse M1. It also does not claim that an independent semantic rereview of the full final `b2d6fe8...` artifact occurred before merge. Machine-readiness work is deferred to M1.2, and schema plus contract validation work is deferred to M2.
