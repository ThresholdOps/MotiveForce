# Deterministic Semantic Compiler Replay Contract

- Project: MøtiveFōrce
- Milestone: M1.2.2
- Status: Accepted
- Scope: Deterministic Semantic Compiler replay
- Project status: Concept / pre-MVP

This document is the accepted M1.2.2 design contract, effective as repository-authoritative content through merge of [PR #23](https://github.com/ThresholdOps/MotiveForce/pull/23). It is not a machine schema, not a compiler implementation, not runtime logging, not executable replay verification, and not a production-readiness claim.

The contract represents accepted M1 and M1.2.1 semantics technically. It MUST NOT silently reinterpret, broaden, narrow, or replace those semantics. Refusal to decide remains valid when a replay representation choice would alter accepted meaning.

## 1. Purpose

The Semantic Compiler is intended to be deterministic. A deterministic claim is reviewable only when one compilation attempt can be reconstructed from a complete, exact, and immutable basis and compared with its original semantic outcome.

This contract defines the conceptual information required to:

- identify the complete replay-affecting input,
- identify the exact compiler and mapping rules used,
- control or exclude nondeterminism,
- reproduce the Semantic Compiler execution,
- compare semantic outcomes without assuming canonical serialization,
- distinguish historical reproducibility from current authority,
- diagnose why an execution cannot be replayed or compared.

It does not define a compiler, event log, storage layer, transport API, machine schema, hash algorithm, canonical serialization, or executable validator.

## 2. Architectural boundary

The accepted authority chain remains:

```text
Source material
  -> Analytical Agent
  -> ProcessIRPackage + CompilationPolicyContext
  -> Semantic Compiler
  -> CompiledSemanticModel + CompilationResult
  -> BPMN Kernel
  -> KernelValidationReport
```

The replay contract applies only to the deterministic Semantic Compiler boundary:

```text
Exact closed semantic input set
+ exact compiler-policy set
+ exact compiler and mapping identities
+ replay-affecting execution parameters
        |
        v
Semantic Compiler
        |
        v
CompiledSemanticModel + CompilationResult
        |
        v
Semantic replay comparison
```

Replay starts from exact accepted records or other records included under an explicitly scoped non-authoritative compilation mode, together with exact compiler-policy inputs.

Semantic Compiler replay MUST NOT claim to reproduce:

- source extraction,
- LLM interpretation,
- candidate generation,
- confidence scoring,
- `RecommendedDecision` generation,
- human `AnalystDecision` creation,
- BPMN Kernel validation,
- `KernelValidationReport`,
- rendering, layout, BPMN DI, or later projections.

The LLM remains outside deterministic compiler replay. The BPMN Kernel remains downstream and has its own validation authority.

## 3. Accepted basis

This accepted contract is based on:

- the accepted [M1 Process IR contract](PROCESS_IR_CONTRACT.md),
- the accepted [M1.2.1 RecordEnvelope and revision-semantics contract](PROCESS_IR_RECORD_ENVELOPE_CONTRACT.md),
- accepted [DEC-0005](../project-memory/decisions/DEC-0005-record-envelope-revision-semantics.md),
- final M1.2.1 review [REV-0004](../project-memory/reviews/M1-2-1-record-envelope-semantic-design-review-3.md),
- final M1.2.2 review [REV-0006](../project-memory/reviews/M1-2-2-deterministic-semantic-compiler-replay-review-2.md),
- tracking [Issue #17](https://github.com/ThresholdOps/MotiveForce/issues/17).

M1 defines the Semantic Compiler input/output and authority boundary. M1.2.1 defines immutable record revisions, exact authoritative bases, integrity descriptors, historical/as-of derivation, and the boundary around authoritative current status.

M1.2.2 consumes those accepted concepts. It does not amend them. If a design choice conflicts with an accepted basis, the affected choice MUST be classified as a potential semantic change and remain unresolved pending human review.

## 4. Core replay invariant

> Given the same exact closed semantic input set, the same exact policy set, the same exact compiler implementation identity, the same exact mapping-ruleset identity, the same exact target BPMN profile basis, and the same replay-affecting execution parameters, the Semantic Compiler MUST produce the same semantic compilation outcome.

Where applicable, the same semantic compilation outcome includes:

- the same compilation outcome,
- the same `requested_scope`,
- the same `authoritative_compiled_scope`,
- the same `non_authoritative_scope`,
- the same `excluded_scope`,
- the same `unresolved_scope`,
- the same semantic BPMN element graph,
- the same semantic element identities,
- the same element types,
- the same connections and relations,
- the same sequence-flow conditions,
- the same participant and lane boundaries,
- the same event semantics,
- the same activity semantics,
- the same mapping-rule provenance,
- the same exact source-revision provenance,
- the same diagnostics under the same diagnostic policy,
- the same `target_bpmn_profile`.

This contract defines semantic determinism, not byte-for-byte identity.

Same-replay verification MUST compare the semantic projection defined by the exact replay-contract revision applicable to the comparison. It MUST NOT compare arbitrary serialization, runtime state, presentation text, or observational metadata. The comparison basis MUST record that exact replay-contract revision or version.

## 5. Determinism distinctions

### Semantic determinism

Semantic determinism means that identical replay-affecting inputs produce semantically equivalent `CompiledSemanticModel` and `CompilationResult` outcomes under this contract.

Semantic determinism is in scope.

### Serialization determinism

Serialization determinism means that a semantic artifact has one canonical machine serialization. No canonical representation is accepted yet.

Serialization determinism and byte identity are deferred to M2 or another accepted machine-representation contract.

### Runtime repeatability

Runtime repeatability concerns whether the compiler can execute reliably in a runtime environment. It includes deployment, dependencies, infrastructure, and availability concerns.

Runtime repeatability is not implemented or operationally specified here. Only replay-affecting dependency identity is in scope.

### Operational observability

Operational observability concerns logs, traces, metrics, timing, and runtime correlation. It may help investigate replay, but it does not define semantic equivalence.

Runtime logging and observability implementation are outside M1.2.2.

## 6. Design-choice classification register

Each material M1.2.2 choice is classified as:

- `M1-derived`,
- `M1.2.1-derived`,
- `Technical representation`,
- `Potential semantic change`.

| Choice ID | Design choice | Classification | Accepted basis | Rationale | Escalation required | Related tracking |
| --- | --- | --- | --- | --- | --- | --- |
| `REPLAY-CHOICE-001` | Replay requires an exact closed semantic and policy input set. | M1.2.1-derived | Exact revisions and exact authoritative bases. | A replay claim cannot depend on inputs that can silently change. | No, unless closure is later used to redefine accepted semantics. | [Issue #17](https://github.com/ThresholdOps/MotiveForce/issues/17), DEC-0006 |
| `REPLAY-CHOICE-002` | Compiler identity requires an immutable implementation or build reference, not a label alone. | Technical representation | M1 requires deterministic compilation but does not define build identity. | A mutable or reused version label cannot prove identical executable semantics. | Resolved and accepted by REV-0006. | [Issue #17](https://github.com/ThresholdOps/MotiveForce/issues/17) |
| `REPLAY-CHOICE-003` | Replay requires an exact immutable mapping-ruleset identity. | M1.2.1-derived | M1 requires mapping-rule provenance; M1.2.1 requires exact immutable references for authoritative bases. | Different rules may produce a different valid mapping from the same business meaning. | Detailed reference schema remains Issue #20. | [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20) |
| `REPLAY-CHOICE-004` | Semantic equivalence is evaluated through the projection defined by the exact applicable replay-contract revision; byte identity is deferred. | Technical representation | No canonical serialization is accepted. | An exact semantic projection bounds replay comparison before a wire format without inventing canonical bytes or a separate comparison-policy artifact. | Resolved and accepted by REV-0006. | [Issue #5](https://github.com/ThresholdOps/MotiveForce/issues/5), [Issue #17](https://github.com/ThresholdOps/MotiveForce/issues/17) |
| `REPLAY-CHOICE-005` | Observational metadata is excluded unless explicitly declared replay-affecting. | Technical representation | M1 compiler outputs are semantic artifacts, not runtime telemetry. | Host, trace, and timing differences do not change business or BPMN semantics. | No, unless an observational field is later used semantically. | [Issue #17](https://github.com/ThresholdOps/MotiveForce/issues/17) |
| `REPLAY-CHOICE-006` | Every potential nondeterministic influence is forbidden, frozen, normalized, or excluded from semantic comparison. | Technical representation | Deterministic compiler boundary. | Unclassified nondeterminism makes replay unverifiable. | Resolved and accepted by REV-0006. | [Issue #17](https://github.com/ThresholdOps/MotiveForce/issues/17) |
| `REPLAY-CHOICE-007` | Historical replay does not establish current authority. | M1.2.1-derived | Historical/as-of derivation and Issue #19 current-status boundary. | Reproducibility proves a past result against past bases, not present validity. | No. Detailed current-status rules remain Issue #19. | [Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19) |
| `REPLAY-CHOICE-008` | Execution with a changed compiler, ruleset, policy, or profile is comparison, not verification of the same replay claim. | Technical representation | Exact basis requirement. | A changed basis tests regression, migration, or compatibility rather than identical replay. | No. | [Issue #17](https://github.com/ThresholdOps/MotiveForce/issues/17) |
| `REPLAY-CHOICE-009` | Generated semantic identifiers must be deterministic from exact inputs and policy or preserved as exact replay inputs only when they were genuine inputs to the original compilation. | Technical representation | Stable compiled element identifiers are required by M1. | Random or environment-derived identifiers would change semantic identity; original output identifiers cannot be injected solely to force equality. | Resolved and accepted by REV-0006. Concrete generation algorithm is deferred. | [Issue #17](https://github.com/ThresholdOps/MotiveForce/issues/17) |
| `REPLAY-CHOICE-010` | Diagnostic reproduction depends on an exact diagnostic-policy reference where policy affects output. | Technical representation | M1 defines diagnostics conceptually; complete policy is deferred. | Diagnostic selection can be replayed only against the same rules. | Complete severity, aggregation, and ordering remain Issue #18. | [Issue #18](https://github.com/ThresholdOps/MotiveForce/issues/18) |

`REPLAY-CHOICE-001` through `REPLAY-CHOICE-010` are accepted by [REV-0006](../project-memory/reviews/M1-2-2-deterministic-semantic-compiler-replay-review-2.md) as part of this contract. `REPLAY-CHOICE-003` remains correctly classified as M1.2.1-derived. Acceptance of `REPLAY-CHOICE-009` does not select an identifier-generation or hashing algorithm. `REPLAY-CHOICE-010` accepts only the exact diagnostic-policy reference requirement; complete diagnostic-policy design remains assigned to Issue #18.

## 7. Scope and explicit non-goals

### In scope

- semantic replay invariant,
- replay input closure,
- `CompilationReplayManifest`,
- `CompilerImplementationRef`,
- replay requirement for `MappingRulesetRef`,
- `ReplayVerificationResult`,
- semantic output equivalence,
- replay-affecting versus observational metadata,
- nondeterminism controls,
- integrity descriptor reuse,
- historical replay versus current authority,
- conceptual replay diagnostics,
- synthetic examples and manual review tests.

### Explicit non-goals

- Semantic Compiler implementation,
- source extraction or LLM replay,
- runtime event logging,
- JSON Schema or another machine schema,
- programming-language classes or interfaces,
- persistence or database design,
- transport API,
- hash algorithm selection,
- canonical JSON, XML, or another serialization,
- byte-for-byte output identity,
- build-system selection,
- package-manager selection,
- signature or attestation implementation,
- complete mapping-rule schema,
- target-profile registry,
- final diagnostic severity enum,
- diagnostic aggregation algorithm,
- detailed partial-compilation dependency algorithm,
- AnalystDecision staleness or invalidation policy,
- executable validation,
- tests or CI.

## 8. Normative terminology

- `replay`: re-execution of the Semantic Compiler from the exact basis captured for an original compilation.
- `replay claim`: assertion that a replay execution uses the same replay-affecting basis as the original.
- `replay input closure`: complete set of exact inputs that can affect Semantic Compiler output.
- `closed basis set`: a basis set whose replay-affecting dependencies are exact, resolved, and enumerated.
- `replay-affecting input`: any semantic record, policy, implementation, ruleset, profile, parameter, or normalized environment basis capable of changing semantic output.
- `observational metadata`: runtime information that observes an execution but MUST NOT affect semantic output unless explicitly classified otherwise.
- `semantic equivalence`: equality of the semantic outcome fields defined by this contract, independent of serialization or observational differences.
- `historical replay`: replay against the exact basis recorded for a past compilation, without claiming that the basis is currently authoritative.
- `same replay verification`: comparison using the same exact replay-affecting basis.
- `regression comparison`: comparison in which compiler implementation, ruleset, policy, profile, or another replay-affecting basis intentionally differs.
- `integrity descriptor`: the accepted M1.2.1 concept identifying digest scope, algorithm, canonicalization profile where applicable, and value.

The terms `latest`, `current`, and repository `HEAD` are not exact replay references.

## 9. CompilationReplayManifest

`CompilationReplayManifest` identifies the complete closed input required to replay one Semantic Compiler execution.

It is a conceptual artifact, not a machine schema and not runtime logging.

### Minimum conceptual content

| Concept | Requirement | Purpose | Notes |
| --- | --- | --- | --- |
| replay-manifest identity | REQUIRED | Identifies the manifest as an addressable artifact. | Exact syntax is deferred. |
| replay-manifest version | REQUIRED | Identifies the manifest contract version. | Does not imply canonical serialization. |
| original compilation request reference | REQUIRED | Connects replay to the requested compilation. | Must resolve exactly where revisioned. |
| `ProcessIRPackage` revision or package-content closure | REQUIRED | Identifies the semantic package basis. | A package label alone is insufficient. |
| exact input record revisions | REQUIRED | Freezes all subject and dependent Process IR records. | Floating `record_id` references are forbidden. |
| exact `RevisionLineage` and `RecordDerivationGraph` edges | REQUIRED when relevant | Reconstructs identity and derivation context. | Historical edges remain explicit. |
| exact status-basis revisions | REQUIRED where eligibility depends on effective status | Reproduces accepted, proposed, deferred, rejected, or superseded basis. | Does not prove current validity. |
| exact value-state assessments | REQUIRED where values affect compilation | Reproduces the four-axis assessment used. | Includes exact subject and basis revisions. |
| exact preservation bases | REQUIRED where an assessment was preserved | Reproduces accepted preservation behavior. | Must satisfy M1.2.1 authority rules. |
| exact `SemanticContext` | REQUIRED | Freezes process, version, variant, perspective, scope, and effective time context. | Context omission is forbidden. |
| exact `CompilationPolicyContext` | REQUIRED | Freezes semantic compiler policy. | Rendering policy is outside replay. |
| exact requested compilation scope | REQUIRED | Defines what was requested. | Must be distinct from result scopes. |
| exact partial-compilation mode | REQUIRED | Records enabled or disabled. | Detailed dependency algorithm is Issue #8. |
| dependency-closure policy reference | REQUIRED when partial compilation is enabled or policy affects scope | Freezes fragment eligibility behavior. | Must resolve exactly. |
| exact target BPMN profile basis | REQUIRED | Freezes the profile used for mapping eligibility. | Detailed profile semantics remain Issue #20. |
| exact mapping-ruleset reference | REQUIRED | Freezes mapping behavior. | No floating current rules. |
| exact compiler implementation/build identity | REQUIRED | Identifies executable semantic behavior. | Human-readable label alone is insufficient. |
| exact compiler semantic-contract version | REQUIRED | Identifies the compiler-facing contract interpretation. | Separate from build identity. |
| diagnostic-policy reference | REQUIRED where diagnostic policy affects output | Freezes diagnostic behavior. | Complete policy remains Issue #18. |
| exact external authoritative bases | REQUIRED when they affect output | Preserves exact external evidence, authority, rules, profiles, or policies. | Uses accepted M1.2.1 exact external-reference forms. |
| integrity descriptors and scopes | REQUIRED where integrity is asserted or checked | Supports integrity verification. | Digest is not evidence or authority. |
| canonicalization-profile references | REQUIRED where a digest depends on canonical form | Makes digest interpretation reproducible. | Concrete canonical form is deferred. |
| replay-affecting execution parameters | REQUIRED | Freezes declared parameters capable of changing semantic output. | Environment defaults are forbidden. |
| original `CompilationResult` reference | REQUIRED | Identifies the report to compare. | Must resolve exactly. |
| original `CompiledSemanticModel` reference | REQUIRED when produced | Identifies the semantic model to compare. | A refused result may have no model. |

The manifest MUST expose the entire replay-affecting basis set.

It MUST NOT silently resolve:

- `latest`,
- `current`,
- mutable URLs,
- repository `HEAD`,
- environment defaults,
- package defaults not frozen in the manifest,
- floating `record_id` references,
- implicit locale, timezone, collation, precision, or identifier policy.

The manifest is not evidence and not authority. Capturing an input proves what was replayed, not that the input was correct or currently authorized.

## 10. CompilerImplementationRef

`CompilerImplementationRef` identifies the exact compiler implementation used by an execution.

A human-readable version label alone is insufficient because labels can be reused, rebuilt, or associated with different dependencies.

The reference MUST support an immutable identity such as one or more of:

- exact source commit,
- immutable build identifier,
- immutable content identifier,
- signed or attested build reference where later available,
- exact dependency manifest reference when dependencies affect semantic behavior,
- exact compiler semantic-contract version.

The identity MUST be sufficient to determine whether two executions used the same compiler semantics. When dependency versions, feature flags, generated code, or build inputs can affect semantics, they belong to the immutable compiler identity or the replay input closure.

This contract does not select a build system, package manager, signature system, attestation format, dependency-lock format, or deployment model.

## 11. MappingRulesetRef

`MappingRulesetRef` identifies the exact mapping rules used by the Semantic Compiler.

For replay, it requires:

- an exact immutable ruleset reference,
- a ruleset version or immutable content identity,
- exact prerequisite-policy bases where those prerequisites affect selection,
- no floating `current rules`, `latest rules`, mutable branch, or repository `HEAD`.

M1.2.2 defines only the replay requirement for exact ruleset identity. It does not define the complete mapping-rule schema, rule lifecycle, prerequisite model, target-profile registry, or profile propagation behavior.

Those detailed rules remain assigned to [Issue #20](https://github.com/ThresholdOps/MotiveForce/issues/20). Issue #20 consumes the exact identity and replay provenance requirements established here.

## 12. ReplayVerificationResult

`ReplayVerificationResult` compares a replay execution with the original compilation.

It is a conceptual comparison report, not a machine enum and not a BPMN validation result.

Conceptual outcomes include:

- `exact semantic match`: replay uses the same complete basis and semantic outcomes match,
- `semantic mismatch`: replay uses the same declared complete basis but semantic outcomes differ,
- `not replayable - input closure incomplete`: one or more replay-affecting inputs are missing,
- `not comparable - basis differs`: compiler, ruleset, policy, profile, or another replay-affecting basis differs,
- `replay execution failed`: the replay could not complete due to an execution failure distinct from semantic mismatch.

The result MUST reference:

- the original compilation,
- the replay execution,
- the replay manifest,
- the original and replay semantic output references,
- the exact replay-contract revision or version defining the semantic comparison projection,
- the exact diagnostic-policy reference where diagnostics affect comparison,
- the original and replay compiler identities,
- the original and replay ruleset identities,
- the original and replay compilation-policy identities,
- the original and replay target-profile identities,
- detected closure or comparability defects,
- replay diagnostics.

These references form the exact comparison basis. This contract does not create a separate comparison-policy artifact or a Replay Verifier component. A future deterministic verification implementation MAY evaluate this contract, but its authority would be limited to replay comparison. It would not establish business truth, evidence validity, current authority, current acceptance, BPMN validity, or `AnalystDecision` validity.

A run using a different compiler build, mapping ruleset, compiler policy, diagnostic policy, or target profile is a regression, migration, or compatibility comparison. It MUST NOT be reported as verification of the same deterministic replay claim.

## 13. Replay input closure

The replay input closure MUST contain every exact input that can affect Semantic Compiler output.

At minimum, the closure MUST evaluate:

- Process IR subject revisions,
- same-record lineage edges,
- cross-record derivation edges,
- effective-status basis records,
- `AnalystDecision` revisions,
- `DecisionAuthorityRef` revisions where compiler eligibility depends on them,
- `SemanticContext` revisions,
- evidence revisions,
- source-artifact revisions where represented in Process IR,
- conditions and condition-result revisions,
- business-rule revisions,
- policy revisions,
- mapping revisions,
- exact external authoritative bases,
- target BPMN profile basis,
- `CompilationPolicyContext`,
- requested scope,
- partial-compilation setting,
- dependency-closure policy,
- mapping ruleset,
- compiler implementation,
- compiler semantic-contract version,
- diagnostic policy,
- canonicalization and digest profiles where integrity comparisons depend on them,
- every replay-affecting execution parameter.

### Closure conditions

| Condition | Meaning | Replay effect |
| --- | --- | --- |
| closure complete | Every replay-affecting dependency is enumerated, exact, resolved, and internally compatible for the historical request. | Replay claim may proceed. |
| closure incomplete | A replay-affecting dependency is absent from the manifest or its scope is unknown. | Replay claim is blocked. |
| dependency present but floating | A dependency is named but resolves through `latest`, `current`, mutable URL, branch head, environment default, or another changing selector. | Replay claim is blocked. |
| dependency unresolved | An exact reference is present but cannot be retrieved or verified sufficiently for replay. | Replay claim is blocked. |
| historical dependency intentionally retained | An exact historical dependency is available although superseded later. | Historical replay may proceed; current authority is not established. |

Missing replay-affecting input MUST block a deterministic replay claim.

Successful resolution of all listed references is necessary but does not prove that an omitted influence does not exist. Compiler design and human review must verify that the closure model is complete for semantic output.

## 14. Historical replay and current authority

Historical replay against an exact closed basis set MAY remain valid when a historical basis has since been superseded.

> Reproducing a historical result proves reproducibility against the recorded historical basis. It does not reauthorize that basis for current authoritative compilation.

Successful historical replay does not establish:

- current acceptance,
- current authority,
- current applicability,
- current mapping eligibility,
- current target-profile validity,
- current validity of an `AnalystDecision`.

[Issue #19](https://github.com/ThresholdOps/MotiveForce/issues/19) remains responsible for:

- staleness,
- invalidation,
- revalidation,
- authority expiry,
- controlled authority carry-forward,
- authoritative current effective status.

Issue #19 remains open, deferred, and not started. M1.2.2 MUST NOT infer current authority when the accepted M1.2.1 boundary requires `EFFECTIVE_STATUS_STALENESS_UNDETERMINED`.

## 15. Semantic output equivalence

Same-replay verification compares the semantic projection defined by the exact replay-contract revision applicable to the comparison. It does not compare arbitrary serialization, runtime state, presentation text, or observational metadata. The exact replay-contract revision or version defining the projection MUST be part of the comparison basis.

No standalone `ReplayComparisonPolicyRef` is introduced. The replay-contract revision itself defines the minimum semantic projection.

### Minimum semantic comparison projection

The projection MUST include, where applicable:

- compilation outcome,
- `requested_scope`,
- `authoritative_compiled_scope`,
- `non_authoritative_scope`,
- `excluded_scope`,
- `unresolved_scope`,
- semantic BPMN graph,
- semantic element types,
- semantic model and element identities defined as part of `CompiledSemanticModel`,
- connections and relations,
- sequence-flow conditions,
- participant and lane boundaries,
- activity and event semantics,
- exact source-revision provenance,
- mapping-rule references and provenance,
- target BPMN profile,
- semantic diagnostic projection under the exact diagnostic policy.

The comparison MUST account for the difference between:

- absent semantic output because compilation was refused,
- an authoritative compiled scope,
- a non-authoritative inspection or planning scope,
- an explicitly permitted partial result,
- excluded and unresolved scope.

### Identifier boundary

Semantic replay comparison MUST distinguish:

- semantic model identifiers,
- semantic element identifiers,
- serialization or container identifiers,
- database and runtime object identifiers,
- execution, run, log, trace, and correlation identifiers.

Only identifiers defined as part of the semantic identity of `CompiledSemanticModel` or its semantic elements are included in semantic equality.

Serialization node IDs, database IDs, runtime object IDs, memory addresses, temporary container IDs, execution IDs, trace IDs, and log correlation IDs are excluded unless a future Accepted contract explicitly makes one semantic.

Generated semantic identifiers MUST be deterministically derived from exact inputs and exact policy. They MAY instead be preserved as exact replay inputs only when they were genuine inputs to the original compilation. A system MUST NOT copy identifiers from the original output into replay input solely to force a match. This contract does not select an identifier-generation algorithm.

### Diagnostic comparison boundary

Under the same exact diagnostic policy, the minimum semantic diagnostic projection MUST include:

- diagnostic code,
- blocking status,
- affected exact records or semantic scope,
- semantic diagnostic parameters that determine the diagnostic's meaning.

Free-text explanation wording, remediation prose wording, localization, formatting, timestamps, log metadata, trace metadata, and incidental ordering MUST NOT create a semantic mismatch by default.

Diagnostic order and multiplicity are compared only when the exact diagnostic policy defines them as semantically significant. [Issue #18](https://github.com/ThresholdOps/MotiveForce/issues/18) remains responsible for final severity vocabulary, aggregation, ordering, deduplication, multiplicity rules, and outcome derivation.

### Semantic versus byte equality

Property order, serialization order, whitespace, encoding layout, graph traversal order, presentation formatting, and observational metadata MUST NOT create a semantic mismatch when the semantic projection is equal.

Conversely, identical-looking bytes or text do not establish semantic equivalence when semantic identity, provenance, scope, conditions, rules, diagnostics, or target profile differ.

Byte identity MUST NOT be required until a future Accepted canonical serialization contract defines canonical bytes.

## 16. Observational metadata boundary

Observational metadata MAY include:

- wall-clock start time,
- wall-clock end time,
- execution duration,
- host name,
- process ID,
- ephemeral run identifier,
- log correlation identifier,
- worker identifier,
- trace identifier.

Differences in observational metadata MUST NOT constitute a semantic replay mismatch unless a field was explicitly declared replay-affecting under an accepted policy.

Observational values MUST NOT affect compiler semantic output.

Runtime object IDs, memory addresses, temporary container IDs, execution IDs, trace IDs, and log correlation IDs are observational by default and are excluded from the minimum semantic comparison projection.

If a field believed to be observational changes semantic output, it is an uncaptured replay dependency and produces `REPLAY_ENVIRONMENT_DEPENDENCY_UNCAPTURED` or `NONDETERMINISTIC_COMPILER_BEHAVIOR`.

## 17. Nondeterminism control

Every potential source of nondeterminism MUST be:

1. forbidden from affecting semantic output,
2. frozen as an exact replay input,
3. normalized under an exact accepted policy, or
4. declared outside semantic comparison.

| Potential source | Required conceptual treatment |
| --- | --- |
| current time | Forbidden from affecting output unless an exact as-of time is frozen as input. |
| random values or seeds | Random behavior is forbidden unless the exact seed and algorithm basis are frozen and accepted; semantic identifiers should not depend on runtime randomness. |
| unordered collection traversal | Normalize under an exact ordering policy or use order-independent semantic construction. |
| locale | Freeze or normalize when parsing, comparison, casing, or formatting can affect semantics. |
| timezone | Freeze or normalize whenever temporal interpretation can affect semantics. |
| Unicode normalization | Use an exact referenced normalization policy when text identity or comparison depends on it. |
| collation | Freeze or normalize when ordering or equality depends on collation. |
| numeric precision and rounding | Freeze exact precision and rounding policy where calculations affect semantic output. |
| concurrency scheduling | MUST NOT affect semantic outcome; race-dependent output is nondeterministic behavior. |
| environment variables | Forbid semantic influence unless each relevant value is captured exactly. |
| filesystem ordering | MUST NOT affect semantic outcome; normalize or sort under an exact policy. |
| network resources | An uncaptured mutable resource MUST NOT be consulted during authoritative replay. |
| mutable external services | Snapshot, version, or replace with exact captured input; live mutable lookup is forbidden. |
| dependency versions | Include in compiler identity or exact replay closure when semantically relevant. |
| generated identifiers | Derive semantic identifiers deterministically from exact inputs and policy, or preserve them as exact replay inputs only when they were genuine inputs to the original compilation. Original output identifiers MUST NOT be injected solely to force a match. |

A compiler MUST NOT consult an uncaptured mutable external source during authoritative replay.

Generated semantic identifiers MUST be deterministic from exact inputs and policy or preserved as exact replay inputs only when they were genuine inputs to the original compilation. Output identifiers MUST NOT be fed back into replay solely to force equality. This contract does not choose a concrete identifier-generation algorithm.

## 18. Digests and integrity

The accepted M1.2.1 integrity rules apply:

- a digest is not evidence,
- a digest is not authority,
- a matching digest does not prove business truth,
- a digest mismatch does not authorize mutation,
- an algorithm reference MUST be explicit when a digest is used,
- a canonicalization-profile reference MUST be explicit when required,
- digest scope MUST be explicit.

A digest MAY support replay integrity by showing that a captured artifact matches an identified byte or canonical-content basis.

A digest MUST NOT substitute for:

- a missing exact revision,
- an unresolved semantic dependency,
- a missing authority basis,
- a missing context,
- a missing mapping ruleset,
- an unidentified compiler build,
- an incomplete replay closure.

This contract does not select a hash algorithm, canonical JSON, canonical XML, serialization technology, or digest encoding.

## 19. Dependency boundaries

### Diagnostic policy - Issue #18

[Issue #18](https://github.com/ThresholdOps/MotiveForce/issues/18) remains responsible for the complete diagnostic severity, blocking, aggregation, ordering, deduplication, multiplicity, and outcome-derivation model.

M1.2.2 requires an exact diagnostic-policy reference where policy affects replay output and requires the minimum semantic diagnostic projection to be reproducible under that policy.

M1.2.2 does not define:

- final severity enum,
- aggregation algorithm,
- partial-compilation outcome aggregation,
- universal diagnostic ordering,
- diagnostic deduplication or multiplicity rules.

Issue #18 remains open, deferred, and not started.

### Partial compilation - Issue #8

[Issue #8](https://github.com/ThresholdOps/MotiveForce/issues/8) remains responsible for the detailed dependency-closure policy for partial compilation.

Replay of partial compilation MUST capture:

- whether partial compilation was enabled,
- requested scope,
- authoritative compiled scope,
- non-authoritative scope,
- excluded scope,
- unresolved scope,
- exact dependency-closure policy reference.

M1.2.2 does not define the full dependency-closure algorithm. Issue #8 remains open, deferred, and not started.

### Current authority - Issue #19

Issue #19 owns detailed staleness, invalidation, revalidation, authority expiry, current effective status, and controlled carry-forward.

Historical replay does not start or complete Issue #19. Issue #19 remains open, deferred, and not started.

### Mapping and target profile - Issue #20

Issue #20 remains responsible for:

- detailed mapping-rule reference semantics,
- mapping-rule versioning,
- satisfied prerequisites,
- target-profile compatibility,
- profile propagation behavior.

M1.2.2 defines only the exact mapping-ruleset and target-profile identity required for replay. Issue #20 consumes these replay requirements and remains open, deferred, and not started.

## 20. Replay diagnostic catalogue

The diagnostics are conceptual. Final severity, aggregation, stable ordering, machine representation, and executable validation are deferred.

| Diagnostic | Meaning | Typical blocking behavior | Affected scope | Expected remediation | Authority implications |
| --- | --- | --- | --- | --- | --- |
| `REPLAY_INPUT_CLOSURE_INCOMPLETE` | One or more replay-affecting inputs are absent or not enumerated. | Blocking for deterministic replay claim. | Entire execution or affected fragment. | Add every missing exact dependency and its role to the manifest. | An incomplete closure cannot verify authoritative compilation. |
| `FLOATING_REPLAY_DEPENDENCY` | A replay dependency uses `latest`, `current`, mutable URL, branch head, environment default, or another floating selector. | Blocking. | Dependency and all output it can affect. | Replace it with an exact immutable reference or captured value. | Floating input cannot support reproducibility or authority. |
| `REPLAY_DEPENDENCY_UNRESOLVED` | An exact dependency reference is recorded but cannot be resolved for replay. | Blocking. | Affected dependency closure. | Restore or provide the exact artifact, or report replay as unavailable. | The system MUST NOT substitute another revision. |
| `COMPILER_IMPLEMENTATION_UNRESOLVED` | The exact compiler implementation or build identity is missing or not immutable. | Blocking for same replay verification. | Entire compiler execution. | Provide immutable source, build, content, dependency, and contract identity as applicable. | Version label alone cannot prove identical compiler semantics. |
| `MAPPING_RULESET_UNRESOLVED` | The exact mapping-ruleset identity is missing, floating, or unavailable. | Blocking. | Affected mappings and compiled scope. | Provide the immutable ruleset reference and prerequisite policy bases. | Mapping provenance and eligibility cannot be reproduced. |
| `REPLAY_POLICY_UNRESOLVED` | A compilation, diagnostic, normalization, or dependency policy affecting output is missing or floating. | Blocking for affected output. | Affected policy scope. | Provide exact policy references and frozen parameters. | Policy defaults MUST NOT be inferred. |
| `TARGET_PROFILE_BASIS_UNRESOLVED` | The exact target BPMN profile basis is missing, floating, or unavailable. | Blocking. | Requested compilation and model comparison. | Provide the exact profile reference and basis. | Mapping eligibility and profile-scoped outcome cannot be reproduced. |
| `REPLAY_ENVIRONMENT_DEPENDENCY_UNCAPTURED` | An environment value or external service affected semantic output but was not captured or normalized. | Blocking. | Entire execution or affected fragment. | Remove the dependency, freeze it, or normalize it under exact policy. | Uncaptured environment cannot support authoritative replay. |
| `NONDETERMINISTIC_COMPILER_BEHAVIOR` | Identical declared complete inputs produce different semantic outcomes, or race/order/random behavior changes output. | Blocking and material defect. | Entire execution or affected fragment. | Identify the hidden influence, correct compiler design, and repeat verification. | Deterministic compiler claim fails for the affected scope. |
| `REPLAY_SEMANTIC_OUTPUT_MISMATCH` | Same comparable replay basis produces a different semantic outcome. | Blocking for verification. | Differing model, result, scope, provenance, profile, or diagnostics. | Investigate compiler behavior, closure completeness, and the semantic projection defined by the applicable replay-contract revision. | Original authority is not automatically revoked, but replay verification fails. |
| `REPLAY_NOT_COMPARABLE` | Compiler, ruleset, policy, profile, or another replay-affecting basis differs. | Blocking for same replay verification; may permit labeled regression comparison. | Comparison as a whole. | Restore the original basis or classify the run as regression, migration, or compatibility comparison. | Changed-basis output cannot verify the original authoritative execution. |
| `REPLAY_INTEGRITY_MISMATCH` | An artifact does not match its recorded integrity descriptor. | Blocking where integrity is required. | Affected artifact and dependent closure. | Investigate provenance, retrieve the correct immutable artifact, and do not mutate history. | Integrity mismatch does not authorize substitution or establish falsity of business meaning by itself. |

## 21. Synthetic examples

All examples are fictional.

### Example A - Successful exact historical replay

A manifest references package revision `PKG-R7`, exact subject and status-basis revisions, context `CTX-R3`, policy `POL-R4`, mapping ruleset `MAP-R9`, target profile `PROFILE-R2`, and compiler build `COMP-B17`. The replay uses the same exact closure and produces the same scopes, graph, provenance, profile, and diagnostics. Observational run IDs differ. The result is `exact semantic match`.

### Example B - Floating latest input

A manifest references `record_id = ACT-100` with resolution `latest`. The current head has changed since the original execution. The system emits `FLOATING_REPLAY_DEPENDENCY` and refuses to guess the original revision.

### Example C - Missing compiler build identity

The original result says compiler version `2.4`, but no immutable source, build, or content identity is available. The label may refer to multiple builds. The system emits `COMPILER_IMPLEMENTATION_UNRESOLVED`.

### Example D - Changed mapping ruleset

The original compilation used `MAP-R9`; a new run uses `MAP-R10`. Even if semantic output matches, the run is a regression or compatibility comparison, not verification of the same replay claim. The result is `REPLAY_NOT_COMPARABLE`.

### Example E - Changed CompilationPolicyContext

The original policy excluded one historical participant; the new policy includes it. The semantic graph differs. Because the policy basis changed, the run is not the same replay and must not be reported as nondeterministic compiler behavior.

### Example F - Serialization and observational differences

Two executions use identical exact replay bases. Property and graph traversal order, whitespace, wall-clock start time, duration, host, execution ID, and trace ID differ. The minimum semantic projection is equal, so the result remains `exact semantic match`.

### Example G - Semantic identifier mismatch

Generated semantic element IDs come from runtime randomness and differ across otherwise identical executions. Because those IDs are defined as semantic element identity, the system emits `NONDETERMINISTIC_COMPILER_BEHAVIOR`. Copying the original output IDs into replay input solely to force equality is invalid; the compiler must derive them deterministically or preserve them only when they were genuine original inputs.

### Example H - Mutable external profile reference

The target profile reference is `https://example.invalid/profiles/current`. The URL is mutable and unversioned. The system emits `TARGET_PROFILE_BASIS_UNRESOLVED` and `FLOATING_REPLAY_DEPENDENCY`.

### Example I - Digest match with unresolved semantic dependency

The package bytes match their recorded digest, but an exact external business-rule basis is unavailable. Digest integrity does not close the semantic dependency. The system emits `REPLAY_DEPENDENCY_UNRESOLVED`.

### Example J - Historical replay does not establish current authority

A 2026-06-01 compilation is reproduced exactly against its historical decisions and context. Later evidence exists and Issue #19 policy has not determined current validity. Historical replay succeeds, but no current authority is inferred.

### Example K - Partial compilation missing closure policy

The original result is `partially-compiled`, and scopes are recorded, but the dependency-closure policy reference is absent. The system emits `REPLAY_INPUT_CLOSURE_INCOMPLETE` and `REPLAY_POLICY_UNRESOLVED`.

### Example L - Semantic mismatch with identical declared inputs

The manifest declares identical complete inputs, compiler build, ruleset, policy, profile, and parameters. The replay produces a different sequence-flow condition. The system emits `REPLAY_SEMANTIC_OUTPUT_MISMATCH` and `NONDETERMINISTIC_COMPILER_BEHAVIOR` until an omitted dependency or compiler defect explains the mismatch.

### Example M - Equivalent diagnostic wording

Original and replay diagnostics have the same code, blocking status, affected exact records, semantic scope, and semantic parameters. Their explanatory and remediation wording differs. Under a diagnostic policy that does not make prose semantic, the diagnostics match.

### Example N - Diagnostic semantic mismatch

Original and replay diagnostics use the same code, but they identify different exact subject revisions and different condition parameters. Their semantic diagnostic projections differ, so the replay emits `REPLAY_SEMANTIC_OUTPUT_MISMATCH`.

## 22. Manual review tests

| Question | Expected answer |
| --- | --- |
| Does the same semantic version label prove the compiler build is identical? | No. Replay requires an immutable compiler implementation or build identity sufficient to identify semantic behavior. |
| Does a matching package digest prove the same business meaning is authoritative? | No. Digest supports integrity, not evidence, business truth, or authority. |
| Can `current mapping rules` be used for historical replay? | No. The exact immutable ruleset used by the original execution is required. |
| Is a run using a newer compiler version verification of the original replay claim? | No. It is a regression, migration, or compatibility comparison. |
| May wall-clock timestamps differ without semantic mismatch? | Yes, when they are observational and were not declared replay-affecting. |
| May locale or collection iteration order affect semantic output? | No. They must be frozen, normalized, or prevented from affecting output. |
| Does successful historical replay make a stale `AnalystDecision` currently valid? | No. Historical reproducibility does not establish current authority; Issue #19 governs staleness. |
| Can the compiler call an uncaptured mutable external service during authoritative replay? | No. Mutable external influences must be frozen, normalized, or forbidden. |
| Can byte identity be required before canonical serialization is accepted? | No. This contract compares semantic outcomes; canonical byte identity is deferred. |
| Can partial compilation be replayed without exact scopes and dependency policy? | No. The mode, scopes, and exact dependency-closure policy are replay-affecting inputs. |
| Does a matching digest replace missing exact references? | No. Integrity cannot substitute for semantic input closure. |
| Does replay include LLM interpretation? | No. Replay begins at the exact Process IR and compiler-policy boundary. |
| If the same declared complete inputs produce different element IDs, is that merely observational? | No. Stable semantic element identity is part of the semantic outcome. |
| If the target profile changes but output appears equivalent, is it the same replay? | No. It is a changed-basis comparison. |
| If every exact historical dependency resolves, is the compilation currently authorized? | Not necessarily. Current authority remains governed by accepted staleness and invalidation policy. |
| Are runtime object IDs part of semantic equality? | No. They are observational unless a future Accepted contract explicitly makes them semantic. |
| Are stable semantic element IDs part of semantic equality? | Yes, where the accepted model defines them as semantic identity. |
| Can identifiers from the original output be injected as replay inputs only to force a match? | No. Preserved identifiers must have been genuine inputs to the original compilation. |
| Do different diagnostic explanations cause a semantic mismatch? | No, unless an Accepted policy defines the text as semantic. |
| Do different diagnostic codes, blocking states, affected scopes, or semantic parameters cause a mismatch? | Yes. Those fields are part of the minimum semantic diagnostic projection. |
| Does property or graph traversal order cause a mismatch? | No, when the semantic graph and complete semantic projection are equivalent. |
| Is byte identity required? | No. Canonical serialization remains deferred. |
| Does a replay comparison result establish current authority or BPMN validity? | No. It has comparison authority only. |

## 23. Resolved human-review questions

Final human semantic and design re-review [REV-0006](../project-memory/reviews/M1-2-2-deterministic-semantic-compiler-replay-review-2.md) resolved:

- The semantic projection is sufficiently determinate.
- The semantic identifier boundary is correct.
- The diagnostic comparison projection is compatible with the future Issue #18 policy.
- The corrected design is ready for acceptance.

## 24. Author self-check and human acceptance

### Author self-check

Author self-check MAY verify:

- required sections are present,
- accepted M1 and M1.2.1 artifacts are unchanged,
- diagnostic codes are defined consistently,
- at least ten synthetic examples are present,
- manual tests cover required boundaries,
- relative links resolve,
- Markdown fences are balanced,
- no machine schema, code, runtime, API, tests, CI, dependency, or algorithm selection was introduced,
- design-choice classifications and dependency boundaries are explicit.

Author self-check is not human semantic review and does not authorize acceptance or merge.

### Human semantic and design acceptance

Human review MUST evaluate:

- replay closure completeness,
- compiler implementation identity,
- mapping-ruleset and target-profile exactness,
- semantic equivalence without canonical bytes,
- environmental nondeterminism controls,
- historical replay versus current authority,
- diagnostic-policy and partial-compilation boundaries,
- whether any choice silently changes accepted M1 or M1.2.1 semantics,
- whether DEC-0006 and this contract should become Accepted.

Human review [REV-0005](../project-memory/reviews/M1-2-2-deterministic-semantic-compiler-replay-review.md) requested the bounded semantic-comparison correction recorded here while retaining the overall architecture.

Final human review [REV-0006](../project-memory/reviews/M1-2-2-deterministic-semantic-compiler-replay-review-2.md) approved reviewed semantic head [`a411692f9a0b4ac754a1a0dd3cfbc3832ae3df08`](https://github.com/ThresholdOps/MotiveForce/commit/a411692f9a0b4ac754a1a0dd3cfbc3832ae3df08), closed `REV5-FIND-001`, accepted `REPLAY-CHOICE-001` through `REPLAY-CHOICE-010`, and authorized bounded finalization and merge.

This document is `Accepted` for M1.2.2 through merge of PR #23. No implementation, schema, Replay Verifier, comparison-policy subsystem, runtime logging, API, persistence, executable validation, tests, CI, identifier algorithm, hashing algorithm, or canonical serialization is authorized.
