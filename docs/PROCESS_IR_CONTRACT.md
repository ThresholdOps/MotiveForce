# Process Intermediate Representation Contract

## 1. Title and status

- Project: MøtiveFōrce
- Milestone: M1
- Status: Accepted
- Scope: Analytical Agent -> Semantic Compiler
- Current project status: Concept / pre-MVP

This document is the semantically accepted M1 design contract. It is not an implementation, not a machine schema, not a production-readiness claim, and not a claim that every future model conforms to every BPMN profile.

## 2. Purpose

The Process Intermediate Representation, abbreviated as `Process IR`, is the explicit boundary between probabilistic interpretation and deterministic semantic compilation.

Its purpose is to make the following rule structurally enforceable:

> The LLM interprets source material but does not validate BPMN.

The Process IR MUST preserve what the source states, what the agent inferred, what remains unresolved, what a human analyst decided, and what the Semantic Compiler accepted or refused. Later deterministic BPMN validation is intentionally outside the Process IR package and belongs to downstream kernel artifacts.

## 3. Position in the architecture

```text
Source material
      |
      v
Analytical Agent
      |
      v
ProcessIRPackage
+ CompilationPolicyContext
      |
      v
Semantic Compiler
      |
      v
CompiledSemanticModel
+ CompilationResult
      |
      v
BPMN 2.0.2 Kernel
      |
      v
KernelValidationReport
```

### Analytical Agent

The Analytical Agent MAY:

- extract atomic statements,
- identify candidate entities and relations,
- normalize terminology,
- propose interpretations,
- propose BPMN mappings,
- assign confidence,
- detect ambiguity,
- detect contradiction,
- ask questions,
- produce a `RecommendedDecision` or a `no-recommendation` outcome.

The Analytical Agent MUST NOT:

- declare BPMN validity,
- silently complete missing process logic,
- resolve material contradictions using confidence alone,
- convert uncertainty into a single authoritative interpretation,
- treat a proposed BPMN type as a validated BPMN element,
- create an authoritative `AnalystDecision`,
- change a record to `accepted` without human authority.

### Semantic Compiler

The Semantic Compiler MAY:

- inspect proposed records for feasibility analysis and diagnostics,
- consume accepted semantic records for authoritative compilation,
- determine whether a proposed BPMN mapping is eligible for compilation,
- map approved business meaning to BPMN concepts,
- produce a `CompiledSemanticModel` when compilation succeeds for the requested scope or for an explicitly permitted partial scope,
- produce compiler diagnostics,
- compile independent model fragments when permitted by the contract.

The Semantic Compiler MUST NOT:

- reinterpret source text,
- invent missing business meaning,
- silently change accepted analyst decisions,
- select one interpretation from unresolved alternatives,
- downgrade unsupported constructs to generic BPMN tasks,
- produce a final authoritative model while blocking issues remain,
- treat agent confidence as human acceptance,
- treat successful compilation as proof that the source interpretation is correct.

### BPMN Kernel

The BPMN Kernel validates a `CompiledSemanticModel` against the declared `target_bpmn_profile`.

The BPMN Kernel MUST NOT reinterpret source evidence, analyst intent, business meaning, or compiler policy.

## 4. Authority model

The Process IR distinguishes proposal, evidence, acceptance, compilation, and validation.

The authority chain is:

- Source evidence establishes what was stated.
- The Analytical Agent proposes interpretations and may recommend, or decline to recommend, a resolution.
- A human analyst with a valid `DecisionAuthorityRef` accepts, rejects, defers, classifies, constrains, or resolves business meaning.
- The Semantic Compiler determines mapping eligibility and maps accepted meaning to BPMN concepts.
- The BPMN Kernel validates BPMN legality.

No component may exercise the authority assigned to another component.

The following distinctions are mandatory:

- agent confidence is not analyst acceptance,
- analyst acceptance is not BPMN validation,
- BPMN validation is not proof that the business interpretation is correct,
- successful compilation is not proof that source ambiguity did not exist,
- a recommended decision is not an `AnalystDecision`,
- a `no-recommendation` outcome is not a resolution,
- an accepted business interpretation is not automatically a valid BPMN mapping.

## 5. Decision authority in M1

For the M1 contract, an `AnalystDecision` is an explicit human decision.

The Analytical Agent MAY produce a `RecommendedDecision`, but such a proposal:

- MUST NOT resolve ambiguity,
- MUST NOT resolve contradiction,
- MUST NOT unblock authoritative compilation,
- MUST NOT change a semantic record to `accepted`,
- MUST NOT supersede evidence,
- MUST NOT be treated as an `AnalystDecision`,
- MUST NOT be treated as human acceptance,
- MUST remain traceable to its rationale and supporting records.

Future versions MAY support delegated or supervised decision agents, but this requires a separate governance decision defining identity, authority, accountability, auditability, escalation, and revocation.

The exact technical representation of analyst identity remains an open implementation decision. The authority model does not remain open in M1: authoritative analytical decisions are human.

`DecisionAuthorityRef` establishes why a human actor is authorized to issue a particular `AnalystDecision` in a specific context and scope. The technical identity-storage mechanism may remain open, but authorization semantics MUST NOT remain open.

## 6. Scope and non-goals

The Process IR contract covers:

- provenance,
- source evidence,
- atomic business statements,
- candidate entities,
- candidate relations,
- normalized terminology,
- proposed BPMN mappings,
- uncertainty,
- missing required information as a derived condition,
- ambiguity,
- contradiction,
- findings,
- unresolved questions,
- recommended decisions,
- analyst decisions,
- semantic contexts,
- decision authority references,
- compiled semantic model boundaries,
- target BPMN profile propagation,
- compiler diagnostics.

Explicit non-goals:

- complete BPMN metamodel representation,
- BPMN XML serialization,
- BPMN DI layout,
- diagram rendering,
- RACI report generation,
- persistence technology,
- workbench user interface,
- knowledge graph implementation,
- JSON or database serialization,
- complete catalogue of BPMN mapping rules,
- automated governance for delegated decision agents,
- implementation of identity, attestation, IAM, certificate, or signature mechanisms.

## 7. Package direction and compiler output

### ProcessIRPackage

A `ProcessIRPackage` represents semantic input and reviewed analytical state consumed by the Semantic Compiler.

It includes source artifacts, evidence fragments, statements, candidate entities, candidate relations, proposed BPMN mappings, findings, unresolved questions, recommended decisions, analyst decisions, semantic contexts, and decision authority references.

It MUST NOT contain authoritative BPMN Kernel validation results.

A `ProcessIRPackage` MAY define a package-level default `SemanticContext`, but the default MUST be explicit. Context inheritance MUST be traceable. A record-specific `context_ref` MUST override the package default explicitly. No compiler behavior may infer context from omission.

### CompilationPolicyContext

M1 selects Option B for `ModelingDecision` placement: modeling decisions belong to a separate conceptual `CompilationPolicyContext`, not to `ProcessIRPackage`.

This option is selected because modeling decisions are compiler policy choices rather than source-derived process meaning. Keeping them outside `ProcessIRPackage` reduces the risk that modeling policy will be mistaken for business evidence.

A `CompilationPolicyContext` MAY contain:

- modeling decisions,
- approved BPMN modeling profile references,
- required `target_bpmn_profile`,
- `partial_compilation_mode`,
- identifier policies,
- requested semantic compilation scope,
- permitted BPMN semantic subset,
- semantic mapping policies,
- policies for selecting between semantically equivalent BPMN representations,
- compiler execution constraints.

A `CompilationPolicyContext` MUST NOT contain presentation-only concerns, including element coordinates, layout direction, colors, fonts, visual spacing, label placement, diagram styling, draw.io-specific rendering rules, report formatting, or other presentation-only rules.

It is associated with a compiler execution. The compiler receives a `ProcessIRPackage` plus, where needed, a `CompilationPolicyContext`, and records which policy context was applied in the `CompilationResult`.

`CompilationPolicyContext` MAY resolve only modeling-policy diagnostics. It MUST NOT resolve business-semantic diagnostics. It MUST NOT contain evidence, replace source clarification, or authorize business meaning.

Trade-off: this keeps process meaning cleaner, but it requires explicit association between package, policy context, and compiler output. This placement decision remains subject to human semantic review.

### CompiledSemanticModel

A `CompiledSemanticModel` is the deterministic semantic model produced by the Semantic Compiler and consumed by the BPMN Kernel.

It is not BPMN XML, BPMN DI, a visual diagram, a rendering policy, or a compiler report.

Minimum conceptual content:

- stable model identifier,
- reference to the source `ProcessIRPackage`,
- reference to the applied `CompilationPolicyContext`,
- `semantic_context_ref`,
- requested scope,
- compiled scope,
- deterministic graph of BPMN semantic elements,
- BPMN semantic element types,
- connections and relations,
- sequence-flow conditions where applicable,
- participant and lane boundaries,
- event semantics,
- activity semantics,
- stable compiled element identifiers,
- provenance references to accepted semantic records,
- references to mapping rules or mapping rationale,
- `target_bpmn_profile`.

The exact machine representation remains outside M1.

`CompiledSemanticModel` is the semantic artifact to validate. `CompilationResult` is the report about the compilation attempt.

### CompilationResult

A `CompilationResult` is a separate conceptual compiler output. It contains at least:

- reference to the input Process IR package,
- reference to the applied `CompilationPolicyContext` where applicable,
- reference to the `CompiledSemanticModel` when one is produced,
- `target_bpmn_profile`,
- requested compilation scope,
- authoritative compiled scope,
- non-authoritative scope,
- excluded scope,
- unresolved scope,
- compilation outcome,
- compiler diagnostics,
- compiled fragment references where applicable,
- provenance links to accepted semantic records.

A refused compilation MAY produce no `CompiledSemanticModel`. A partial compilation MAY produce a scoped `CompiledSemanticModel` only under the explicit partial-compilation policy defined by this contract.

### KernelValidationReport

A `KernelValidationReport` is a later downstream artifact outside the Process IR contract. It contains deterministic BPMN validation results.

It MUST reference the validated `CompiledSemanticModel` and the `target_bpmn_profile` used by the BPMN Kernel.

### RenderingPolicyContext

A `RenderingPolicyContext` is a future downstream artifact or configuration context for BPMN DI generation, layout, visual styling, draw.io projection, and report presentation.

`RenderingPolicyContext` is outside the M1 Process IR contract. It is not an input to semantic meaning acceptance, is not evidence, is not part of `ProcessIRPackage`, and is not required to determine BPMN semantic validity.

The conceptual artifact flow is:

```text
ProcessIRPackage
+ CompilationPolicyContext
        |
        v
Semantic Compiler
        |
        v
CompiledSemanticModel
+ CompilationResult
        |
        v
BPMN Kernel
        |
        v
KernelValidationReport
        |
        v
Later projection and rendering
```

The BPMN Kernel validates the `CompiledSemanticModel` against the declared `target_bpmn_profile`. The Kernel MUST NOT reinterpret source evidence or analyst intent.

### target_bpmn_profile

`target_bpmn_profile` identifies the BPMN conformance or modeling profile against which compilation eligibility and kernel validation are evaluated.

M1 does not claim one universal meaning of `BPMN-valid`. Mapping eligibility depends on the target profile. Kernel validation is scoped to the target profile. A model valid for one profile is not automatically valid for another.

The profile reference is REQUIRED in:

- `CompilationPolicyContext`,
- compilation request,
- `CompiledSemanticModel`,
- `CompilationResult`,
- `KernelValidationReport`.

The same profile reference MUST propagate across the pipeline unless an explicit compatible profile transformation is recorded.

M1 may refer conceptually to profiles such as Descriptive, Analytic, Common Executable, full Process Modeling profile, or organization-specific approved subset. M1 does not define a profile registry.

This document does not define implementation-specific serialization or field types.

## 8. Contract envelope

A `ProcessIRPackage` MUST include, at minimum:

| Collection | Purpose |
| --- | --- |
| `ir_version` | Identifies the Process IR contract version used by the package. |
| `package_id` | Provides a stable identity for the package. |
| `process_scope` | Describes the process, fragment, or analysis boundary covered by the package. |
| `default_context_ref` | Optionally identifies an explicit package-level `SemanticContext`. |
| `semantic_contexts` | Defines contexts for interpreting contextual statements, values, decisions, findings, mappings, and compilation requests. |
| `decision_authority_refs` | Defines why a human actor is authorized to issue an `AnalystDecision` for a specific context and scope. |
| `source_artifacts` | Lists input documents, workshop clarifications, interview responses, process-owner statements, or other sources available to the analysis. |
| `evidence_fragments` | Stores addressable source fragments with preserved original wording. |
| `statements` | Stores atomic source-derived business assertions. |
| `candidate_entities` | Stores proposed process, business, role, system, data, and rule entities. |
| `candidate_relations` | Stores proposed relationships between records. |
| `proposed_bpmn_mappings` | Stores non-authoritative proposed BPMN mappings. |
| `findings` | Stores material ambiguity, contradiction, missing-information, and conflict records. |
| `unresolved_questions` | Stores questions requiring additional evidence or human decision. |
| `recommended_decisions` | Optionally stores non-authoritative recommendations or `no-recommendation` outcomes produced by the Analytical Agent. |
| `analyst_decisions` | Stores explicit human decisions that accept, reject, defer, classify, constrain, or resolve business meaning. |

A Process IR package MAY contain zero or more recommended decisions. Absence of a recommendation is a valid analytical outcome. A recommendation does not imply that the issue is resolved. `recommended_decisions` and `analyst_decisions` MUST remain separate collections. No compiler behavior may infer acceptance from the presence of a recommendation.

This contract does not define implementation-specific field types. All records require stable identifiers within the package. Omission MUST NOT be used to represent value state. Unresolved information MUST be explicit. References MUST remain traceable across review and compilation. Context-sensitive records MUST have an explicit or inherited `context_ref`.

## 9. Core record types

### 9.1 SemanticContext

`SemanticContext` defines the explicit context in which a semantic assertion, value state, finding, decision, mapping, or compilation request is interpreted.

Terms such as `required`, `optional`, `conditional`, `not-applicable`, `current`, `historical`, `accepted`, `superseded`, process version, process variant, and modeled scope have no authoritative meaning without an explicit context.

Minimum conceptual content:

- stable `context_id`,
- `process_ref`,
- `process_version_ref` where applicable,
- perspective,
- organizational scope,
- effective time scope,
- modeled scope,
- `variant_ref` where applicable,
- `parent_context_ref` where inheritance is used,
- rationale or evidence for context selection.

Perspective MAY use conceptual values such as `AS-IS`, `TO-BE`, `TRANSITION`, or `OTHER`. M1 does not define a machine enum.

Records whose meaning can vary by context MUST carry or inherit `context_ref`. This includes value-state assessments, contextual `AtomicStatement` interpretations, accepted `CandidateEntity` records, accepted `CandidateRelation` records, `Finding`, `UnresolvedQuestion`, `RecommendedDecision`, `AnalystDecision`, `ProposedBPMNMapping`, and compilation request scope.

### 9.2 SourceArtifact

`SourceArtifact` represents an input document or source.

Minimum conceptual content:

- stable identifier,
- source type,
- source name,
- source version or digest where available,
- language,
- provenance metadata.

When a human provides new business information, it MUST be recorded conceptually as a new `SourceArtifact`, such as a workshop clarification, interview response, or process-owner statement.

### 9.3 EvidenceFragment

`EvidenceFragment` represents an addressable fragment of a source.

Minimum conceptual content:

- stable identifier,
- reference to the source artifact,
- source locator,
- preserved original wording,
- extraction method,
- optional integrity digest.

The source locator MAY be a page, paragraph, heading, table cell, timestamp, line range, XML path, or another source-specific location.

Evidence fragments MUST be immutable. A corrected interpretation MUST create a new interpretation record rather than modify the source fragment.

### 9.4 AtomicStatement

`AtomicStatement` represents one indivisible source-derived business assertion.

Minimum conceptual content:

- stable identifier,
- normalized statement,
- original evidence references,
- statement category,
- extraction confidence,
- value-state dimensions where applicable,
- `context_ref` where interpretation is contextual,
- optional subject, predicate, and object references.

A statement MUST NOT combine several independently disputable claims. Every source-derived atomic statement MUST reference at least one evidence fragment.

### 9.5 CandidateEntity

`CandidateEntity` represents an entity proposed by the Analytical Agent.

Candidate entity kinds SHOULD include at least:

- activity,
- event,
- decision,
- participant,
- role,
- system,
- business data object,
- business rule,
- phase,
- process,
- subprocess.

Minimum conceptual content:

- stable identifier,
- candidate kind,
- canonical proposed name,
- preserved source names and aliases,
- description,
- supporting statements,
- evidence references,
- lifecycle status,
- resolution state,
- `context_ref` when accepted or when contextual interpretation is required.

A normalized name MUST NOT erase original wording.

### 9.6 CandidateRelation

`CandidateRelation` represents a proposed relationship between entities or statements.

Relation kinds SHOULD include at least:

- precedes,
- follows,
- triggers,
- produces,
- consumes,
- performed-by,
- accountable-by,
- consulted-role,
- informed-role,
- uses-system,
- conditional-on,
- parallel-with,
- mutually-exclusive-with,
- part-of,
- sends-to,
- receives-from,
- supports,
- contradicts,
- supersedes.

Minimum conceptual content:

- stable identifier,
- relation kind,
- source reference,
- target reference,
- qualifiers,
- evidence references,
- confidence,
- resolution state,
- `context_ref` when accepted or when contextual interpretation is required.

### 9.7 ProposedBPMNMapping

`ProposedBPMNMapping` represents a non-authoritative proposal for mapping approved or candidate business meaning to BPMN.

Minimum conceptual content:

- stable identifier,
- referenced semantic records,
- proposed BPMN concept,
- mapping rationale,
- required facts,
- missing facts,
- alternatives,
- evidence references,
- proposal status,
- `context_ref`,
- `target_bpmn_profile` where proposed eligibility depends on profile.

A `ProposedBPMNMapping` is not a BPMN element and is not proof of BPMN validity.

The Analytical Agent MAY propose Task, Event, Gateway, Sequence Flow, Message Flow, Participant, Lane, Data Object, Sub-Process, or another BPMN concept. The Semantic Compiler determines whether the mapping is `eligible-for-compilation`. The BPMN Kernel determines whether the resulting BPMN model is valid.

### 9.8 Finding

`Finding` represents a material analytical issue.

Finding kinds SHOULD include:

- ambiguity,
- contradiction,
- missing information,
- terminology conflict,
- sequencing conflict,
- scope conflict,
- responsibility conflict,
- historical content,
- proposed deletion,
- unsupported interpretation.

Minimum conceptual content:

- stable identifier,
- finding kind,
- affected records,
- evidence references,
- description,
- blocking status,
- resolution state,
- possible remediation,
- `context_ref`.

### 9.9 UnresolvedQuestion

`UnresolvedQuestion` represents a question requiring additional evidence or human decision.

Minimum conceptual content:

- stable identifier,
- question,
- reason,
- affected records,
- required answer type,
- blocking status,
- resolution state,
- `context_ref`.

### 9.10 RecommendedDecision

`RecommendedDecision` represents a non-authoritative decision recommendation or `no-recommendation` outcome produced by the Analytical Agent.

M1 represents `no-recommendation` as a `RecommendedDecision` record whose `recommendation_outcome` is `no-recommendation` and whose selected interpretation is absent.

Minimum conceptual content:

- stable identifier,
- decision subject,
- recommendation outcome: `recommended` or `no-recommendation`,
- recommended interpretation when outcome is `recommended`,
- alternatives,
- rationale,
- supporting records,
- confidence metadata,
- known limitations,
- `context_ref`.

A `RecommendedDecision`:

- MUST NOT resolve ambiguity,
- MUST NOT resolve contradiction,
- MUST NOT unblock authoritative compilation,
- MUST NOT change semantic records to `accepted`,
- MUST NOT supersede evidence,
- MUST NOT be treated as an `AnalystDecision`,
- MUST NOT be treated as human acceptance,
- MUST remain traceable to its rationale and supporting records.

When material ambiguity or contradiction exists, a difference in confidence alone MUST NOT be sufficient to create a `RecommendedDecision` selecting one interpretation.

The Analytical Agent MAY issue a recommendation only when its rationale includes at least one relevant criterion beyond the confidence score, such as source authority, source recency, explicit lifecycle status, applicability to the current process version, analyst-provided policy, corroborating independent evidence, or formally defined precedence rules.

Confidence MAY be included as metadata, but MUST NOT serve as the sole decision rationale.

`no-recommendation` is the outcome used when the agent cannot responsibly prefer one interpretation. It preserves all alternatives, leaves the finding unresolved, does not unblock compilation, and SHOULD explain why no responsible recommendation can be made.

### 9.11 DecisionAuthorityRef

`DecisionAuthorityRef` establishes why a human actor is authorized to issue a particular `AnalystDecision` in a specific context and scope.

Minimum conceptual content:

- `actor_ref`,
- `actor_type`,
- `authority_role`,
- `authority_scope`,
- `authority_source_ref`,
- effective time scope,
- `attestation_ref` where available,
- `context_ref`.

For M1, `actor_type = human` is REQUIRED for authoritative `AnalystDecision` records.

Authority scope MUST be able to constrain at least process, process version, semantic context, decision category, organizational scope, and effective time.

Every authoritative `AnalystDecision` MUST reference a valid `DecisionAuthorityRef`.

A decision MUST NOT be treated as authoritative when actor type is not human in M1, authority scope does not cover the decision, authority is expired or not yet effective, authority source is missing, context does not match, or required attestation is absent under the applicable policy.

M1 does not define IAM, certificate, signature, or identity-storage implementation.

### 9.12 AnalystDecision

`AnalystDecision` represents an explicit human resolution.

Minimum conceptual content:

- stable identifier,
- decision subject,
- `decision_outcome`,
- selected interpretation where required by outcome,
- rejected alternatives where applicable,
- rationale,
- analyst identity or actor reference,
- valid `DecisionAuthorityRef`,
- decision timestamp,
- effective time,
- supporting evidence,
- `context_ref`,
- superseded decisions where applicable.

Allowed conceptual `decision_outcome` values are `accept`, `reject`, `defer`, `resolve`, `classify`, and `constrain-scope`. M1 does not define a machine enum.

Conditional content rules:

- `selected_interpretation` is REQUIRED for `accept` and `resolve` when an interpretation is selected,
- `rejected_alternatives` MAY be present for `accept`, `reject`, and `resolve`,
- `defer` requires a reason and review condition,
- `classify` requires the classification and context,
- `constrain-scope` requires included and excluded scopes,
- `reject` MAY reject without selecting a replacement.

All decision outcomes MUST include rationale, evidence references where business meaning is affected, `DecisionAuthorityRef`, `context_ref`, effective time, and supersession references where applicable.

An `AnalystDecision` MUST NOT use `ModelingDecision` outcomes.

An analyst decision MUST NOT erase the original ambiguity or contradiction. It resolves the issue for compilation while preserving the full provenance chain.

An `AnalystDecision` MAY select between supported interpretations, reject an interpretation, constrain process scope, classify content as current, historical, or superseded, or resolve a conflict between evidence-backed alternatives.

An `AnalystDecision` MUST NOT replace evidence for a claim about business reality.

### 9.13 ModelingDecision

`ModelingDecision` records a deliberate modeling choice that does not claim a new business fact.

Examples include:

- selecting one of several semantically equivalent BPMN representations,
- limiting the compiled diagram scope,
- choosing a semantic compilation scope,
- choosing a stable identifier convention,
- applying an approved modeling profile.

A `ModelingDecision`:

- MUST NOT fabricate business meaning,
- MUST reference the accepted semantics or policy it applies to,
- MUST remain separate from evidence,
- MUST NOT be used to resolve unsupported business assertions,
- MUST remain distinct from BPMN validation.

In M1, `ModelingDecision` is placed in `CompilationPolicyContext`, not in `ProcessIRPackage`.

### 9.14 CompilerDiagnostic

`CompilerDiagnostic` is Semantic Compiler output associated with Process IR records.

Minimum conceptual content:

- diagnostic code,
- severity,
- blocking status,
- affected records,
- explanation,
- required remediation.

Compiler diagnostics are not agent findings, although they MAY reference the same records.

## 10. Multi-axis value-state model

The previous single-axis `QualifiedValue<T>` pattern is replaced by separate conceptual dimensions. This prevents epistemic state, applicability, requirement, and value presence from being collapsed into one enum.

### 10.1 Dimensions

`knowledge_state` describes what is known about interpretation:

- `known`,
- `unknown`,
- `ambiguous`,
- `contradictory`.

`applicability` describes whether the value applies in the relevant `SemanticContext`:

- `applicable`,
- `not-applicable`,
- `undetermined`.

`requirement_state` describes whether the value is required in the relevant `SemanticContext`:

- `required`,
- `optional`,
- `conditional`,
- `undetermined`.

`value_presence` describes whether a value or alternatives are present:

- `present`,
- `absent`.

`unknown` is epistemic. `missing` is not an epistemic state. `not-applicable` is not an epistemic state. Omission is not a knowledge state. The dimensions may combine. Downstream diagnostics are derived from combinations of these dimensions.

Known absence means available evidence or an explicit applicable rule establishes that the value does not exist in the relevant context. Examples include an activity known not to use a system, a sequence flow known not to be the default flow, a review known not to be required for the current case, an event known not to carry a message, or an optional performer explicitly absent.

A known absence MUST be supported by evidence or an explicit applicable rule, identify the context in which absence is established, not be represented through omission alone, not be confused with `unknown`, and not automatically produce a missing-information diagnostic.

For every value whose applicability is `applicable` and whose `requirement_state` is `required`, `value_presence` MUST be `present`.

Missing required information is a derived condition:

```text
applicability = applicable
AND requirement_state = required
AND value_presence = absent
```

This condition produces `MISSING_REQUIRED_INFORMATION`.

The system may know a required value is absent. Knowledge of absence does not satisfy the requirement.

Values whose applicability is evidence-backed or rule-backed `not-applicable` are excluded from requirement evaluation for that context. `required + not-applicable` is invalid for the same active context. Changing applicability requires evidence or an applicable rule. `not-applicable` MUST NOT be used as a manual escape from missing required information.

`known absence` is not `not-applicable`. `known absence` is not `unknown`. `known absence` does not satisfy a required value.

### 10.2 Combination-validity rules

The model does not treat all theoretical combinations as valid.

| Rule area | Combination | Validity | Diagnostic or required handling |
| --- | --- | --- | --- |
| Value-presence consistency | `knowledge_state = known` with `value_presence = present` | Valid. | The value may be used if other conditions allow. |
| Value-presence consistency | `knowledge_state = known` with `value_presence = absent`, `applicability = applicable`, `requirement_state = optional` | Valid when absence itself is the evidence-backed fact. | Treat as known absence; no missing-information diagnostic. |
| Value-presence consistency | `knowledge_state = known` with `value_presence = absent`, `applicability = applicable`, `requirement_state = conditional` and condition known false | Valid when the inactive condition is evidence-backed or rule-backed. | Treat as known conditional absence; no missing-information diagnostic. |
| Value-presence consistency | `knowledge_state = known` with `value_presence = absent`, `applicability = applicable`, `requirement_state = required` | Valid as knowledge of absence, but invalid as satisfying the requirement. | `MISSING_REQUIRED_INFORMATION`; knowledge of absence does not satisfy a required value. |
| Value-presence consistency | `knowledge_state = known` with `value_presence = absent` without evidence, rule, or context for absence | Invalid. | `INVALID_VALUE_STATE_COMBINATION`. |
| Value-presence consistency | `knowledge_state = ambiguous` | Valid only when at least two plausible alternatives are present. | `AMBIGUOUS_BUSINESS_MEANING` until resolved. |
| Value-presence consistency | `knowledge_state = contradictory` | Valid only when incompatible supported claims or alternatives are present. | Contradiction diagnostic such as `CONTRADICTORY_SEQUENCE` or `CONTRADICTORY_RESPONSIBILITY`. |
| Value-presence consistency | `knowledge_state = unknown` with `value_presence = absent` | Valid. | May produce a blocking diagnostic if downstream use requires the value. |
| Value-presence consistency | `knowledge_state = unknown` with `value_presence = present` | Conditionally valid when a raw value exists but its semantic interpretation is unknown. | Rationale required; default diagnostic SHOULD be `UNRESOLVED_INTERPRETATION` when interpretation is required. It MUST NOT automatically become ambiguity. |
| Applicability consistency | `applicability = not-applicable` with `value_presence = absent` | Normally valid. | No missing-information diagnostic. |
| Applicability consistency | `applicability = not-applicable` with `value_presence = present` | Invalid unless retained solely as historical or superseded provenance. | Exception MUST be explicit; otherwise `INVALID_VALUE_STATE_COMBINATION`. |
| Applicability consistency | `requirement_state = required` with `applicability = not-applicable` for the same active context | Invalid. | `INVALID_VALUE_STATE_COMBINATION`. |
| Applicability consistency | `applicability = undetermined` when applicability affects mapping legality | Conditionally valid in Process IR, but blocking for authoritative compilation. | `UNRESOLVED_OPTIONALITY` or related diagnostic. |
| Requirement consistency | `requirement_state = required`, `applicability = applicable`, `value_presence = absent` | Derived missing required information. | `MISSING_REQUIRED_INFORMATION`. |
| Requirement consistency | `requirement_state = conditional` without a referenced condition | Conditionally valid in Process IR, but blocking if needed downstream. | `UNRESOLVED_OPTIONALITY`. |
| Requirement consistency | `requirement_state = undetermined` and downstream behavior depends on it | Conditionally valid in Process IR, but blocking for authoritative compilation. | `UNRESOLVED_OPTIONALITY`. |
| Contradiction and ambiguity consistency | `knowledge_state = ambiguous` with fewer than two plausible alternatives | Invalid. | `INVALID_VALUE_STATE_COMBINATION`. |
| Contradiction and ambiguity consistency | `knowledge_state = contradictory` without at least two materially incompatible supported claims | Invalid. | `INVALID_VALUE_STATE_COMBINATION`. |

Confidence MUST NOT collapse `ambiguous` or `contradictory` into `known`.

`unknown` means interpretation cannot currently be determined. `ambiguous` means at least two plausible interpretations exist. `contradictory` means at least two materially incompatible supported claims exist. `ambiguity` is an analytical condition and finding category. `AMBIGUOUS_BUSINESS_MEANING` is the normative Semantic Compiler diagnostic emitted when unresolved ambiguity affects compilation.

### 10.3 Conceptual examples

Required performer cannot be determined:

- `knowledge_state`: `unknown`
- `applicability`: `applicable`
- `requirement_state`: `required`
- `value_presence`: `absent`
- derived diagnostic: `MISSING_REQUIRED_INFORMATION`

Known optional absence:

- `knowledge_state`: `known`
- `applicability`: `applicable`
- `requirement_state`: `optional`
- `value_presence`: `absent`
- result: valid known absence

Known required absence:

- `knowledge_state`: `known`
- `applicability`: `applicable`
- `requirement_state`: `required`
- `value_presence`: `absent`
- result: `MISSING_REQUIRED_INFORMATION`

Unknown absence:

- `knowledge_state`: `unknown`
- `applicability`: `applicable`
- `requirement_state`: `required`
- `value_presence`: `absent`
- result: `MISSING_REQUIRED_INFORMATION` and unresolved knowledge

Escalation code does not apply to a plain task:

- `applicability`: `not-applicable`
- `requirement_state`: `optional` or `undetermined` according to context
- `value_presence`: `absent`
- derived diagnostic: none for missing information

Two incompatible performers are supported:

- `knowledge_state`: `contradictory`
- `applicability`: `applicable`
- `requirement_state`: `required`
- `value_presence`: `present` through incompatible alternatives
- derived diagnostic: `CONTRADICTORY_RESPONSIBILITY`

Raw label exists but meaning is unknown:

- `knowledge_state`: `unknown`
- `applicability`: `applicable`
- `requirement_state`: `optional` or `required` according to context
- `value_presence`: `present`
- required handling: rationale explaining that a raw value exists but its semantic interpretation is unknown; diagnostic `UNRESOLVED_INTERPRETATION` when interpretation is required

A future machine schema MUST encode or validate these compatibility rules.

## 11. Record lifecycle

Agent-produced records use these lifecycle states:

- `proposed`,
- `under-review`,
- `accepted`,
- `rejected`,
- `deferred`,
- `superseded`.

`accepted` means accepted as business meaning, not validated as BPMN. Only authorized human action may move business meaning to `accepted` in M1. Rejected records remain in the provenance history. Superseded records remain traceable to their replacements. Unresolved records MUST NOT become accepted implicitly.

Mapping proposal states are:

- `proposed`,
- `eligible-for-compilation`,
- `rejected`,
- `blocked`,
- `superseded`.

`eligible-for-compilation` is assigned by the Semantic Compiler. It requires accepted business meaning, resolved references, compatible `SemanticContext`, declared `target_bpmn_profile`, and no relevant blocking diagnostics. It is not a human business decision, is not BPMN validation, and does not mean `BPMN-valid`.

## 12. Evidence rules

The following invariants are mandatory:

- Every source-derived atomic statement MUST reference at least one evidence fragment.
- Every accepted source-derived semantic assertion MUST reference evidence.
- Every accepted source-derived entity or relation MUST trace to evidence.
- An `AnalystDecision` MAY additionally explain how conflicting or ambiguous evidence was resolved.
- Analyst decisions MUST reference the records and evidence they resolve.
- An `AnalystDecision` MUST NOT replace evidence for a claim about business reality.
- When a human provides new business information, record it conceptually as a new `SourceArtifact`, one or more `EvidenceFragment` records, related `AtomicStatement` records, and an `AnalystDecision` where a decision is still required.
- Contradicting evidence MUST remain preserved after resolution.
- Confidence is metadata, not evidence.
- High confidence MUST NOT resolve a material contradiction automatically.
- Normalization MUST preserve source aliases and original wording.
- Historical and deleted content MUST be represented by status rather than silently removed.
- Evidence fragments MUST remain immutable.
- Corrected interpretation creates a new record rather than changing the evidence.
- Rejected and superseded interpretations MUST remain traceable.
- Compilation output MUST retain links to accepted semantics and their evidence.

## 13. Proposed-record inspection boundary

The Semantic Compiler MAY inspect `proposed` records only for:

- feasibility analysis,
- diagnostic generation,
- identification of missing facts,
- comparison of alternative mappings,
- creation of a non-authoritative compilation plan.

The Semantic Compiler MUST NOT use merely `proposed` business meaning to produce an authoritative compiled fragment.

Authoritative compilation requires accepted semantic meaning.

`proposed` is inspectable. `accepted` is compilable, subject to all other conditions. `rejected`, `deferred`, and unresolved records are not authoritative compilation inputs.

Attempted authoritative use of proposed records MUST produce `PROPOSED_RECORD_NOT_AUTHORITATIVE`.

## 14. Contract invariants

The Process IR contract requires these invariants:

- Stable identifiers are unique within a Process IR package.
- References must resolve or produce a blocking diagnostic.
- No implicit semantic defaults are permitted.
- No compiler behavior may infer context from omission.
- Context-sensitive records require an explicit or inherited `context_ref`.
- Terms such as `required`, `optional`, `not-applicable`, `current`, `historical`, and `accepted` require `SemanticContext`.
- Authoritative `AnalystDecision` records require a valid `DecisionAuthorityRef`.
- No BPMN type may be inferred solely because other information is absent.
- Confidence is metadata, not authority.
- Confidence alone cannot produce a material recommendation.
- No recommendation is a valid agent outcome.
- A value may be known to be absent.
- Known absence must be explicit and evidence-backed.
- Known absence does not satisfy a required value.
- For every value whose applicability is `applicable` and whose `requirement_state` is `required`, `value_presence` MUST be `present`.
- `not-applicable` must be evidence-backed or rule-backed and must not be used as a manual escape from missing required information.
- Every accepted source-derived assertion has evidence.
- `AnalystDecision` does not replace evidence.
- `ModelingDecision` cannot remediate insufficient business evidence.
- Business-semantic diagnostics and modeling-policy diagnostics are distinct.
- `CompilationPolicyContext` MAY resolve only modeling-policy diagnostics.
- `CompilationPolicyContext` MUST NOT resolve business-semantic diagnostics.
- The agent cannot mark a model or mapping as BPMN-valid.
- The agent cannot create an authoritative `AnalystDecision`.
- The compiler cannot silently mutate accepted semantic records.
- The compiler cannot treat a `RecommendedDecision` as accepted authority.
- Proposed records may be inspected but not authoritatively compiled.
- Mapping eligibility belongs to the Semantic Compiler.
- BPMN validity belongs to the BPMN Kernel.
- `ProcessIRPackage`, `CompiledSemanticModel`, `CompilationResult`, and `KernelValidationReport` are separate conceptual artifacts.
- Kernel validation results do not belong in `ProcessIRPackage`.
- Missing required information is determined by requirement, applicability, and presence, not by knowledge state alone.
- Invalid four-axis combinations produce diagnostics.
- `ModelingDecision` placement must be explicit.
- Modeling decisions do not create business facts.
- `CompilationPolicyContext` affects semantic compilation only.
- Presentation and rendering policy belong to a downstream context.
- Unknown interpretation is distinct from ambiguity.
- A present raw value does not imply its semantic interpretation is known.
- Ambiguity requires at least two plausible interpretations.
- Contradiction requires at least two incompatible supported claims.
- Every compiler diagnostic must reference affected Process IR records.
- Every final compiled element must trace back to accepted semantics and evidence.
- Unresolved blocking findings prevent authoritative compilation.
- Partial compilation is disabled by default and requires explicit `CompilationPolicyContext` enablement.
- Unsupported constructs must produce diagnostics rather than generic substitutions.
- Provenance must survive normalization, review, compilation, and later export.
- Successful BPMN validation does not retroactively remove source ambiguity or contradiction.
- Human authority is required to resolve material semantic conflicts in M1.

## 15. Compiler acceptance contract

A record may be used for authoritative compilation when:

- its semantic meaning is accepted,
- accepted source-derived assertions are evidence-backed,
- required references resolve,
- applicable `SemanticContext` references are compatible,
- required value-state dimensions are compatible,
- required applicable values are present in the active context,
- known-absence states are optional or conditionally inactive in the active context,
- no blocking unresolved finding affects the mapping,
- any required `AnalystDecision` exists and references a valid `DecisionAuthorityRef`,
- the proposed BPMN mapping is `eligible-for-compilation`,
- `target_bpmn_profile` is declared and compatible with the requested mapping.

The compiler MUST refuse authoritative compilation for every requested scope or fragment affected by any of the following conditions:

- insufficient evidence,
- missing semantic context,
- semantic context mismatch,
- missing decision authority,
- decision authority scope mismatch,
- unresolved interpretation of a present raw value when interpretation is required,
- unresolved contradictory sequence,
- ambiguous business meaning,
- ambiguous gateway semantics,
- missing required participant or role,
- unresolved optionality,
- unresolved business cardinality,
- unresolved event trigger,
- unresolved participant identity,
- unresolved source or target reference,
- unsupported mapping,
- human decision required,
- proposed records used as authoritative input,
- ineligible mapping proposal,
- invalid value-state combination,
- missing modeling policy required for semantic compilation,
- missing target BPMN profile,
- target BPMN profile mismatch,
- missing partial-compilation policy where partial compilation is requested,
- blocked dependency closure for a partial compilation fragment.

Blocking diagnostics outside an independent fragment do not block that fragment when partial compilation is explicitly enabled and all partial-compilation conditions are satisfied. This rule does not permit hidden dependencies: the dependency closure of the fragment MUST remain free of blocking diagnostics, the authoritative result is limited to `authoritative_compiled_scope`, the overall result remains `partially-compiled`, and the result MUST NOT be represented as the complete requested process model.

Refusal is a valid and expected result. The compiler MUST prefer refusal over invention.

The Semantic Compiler accepts valid known-absence states where the value is optional or conditionally inactive. It refuses compilation when a required applicable value is absent, even if absence is known. It emits `UNRESOLVED_INTERPRETATION` when a present raw value lacks determined meaning. It emits `MODELING_POLICY_REQUIRED` when accepted business meaning cannot be compiled without a missing modeling policy. It does not treat `ModelingDecision` as evidence and does not consume rendering policy as semantic compilation input.

## 16. Diagnostic catalogue

| Code | Meaning | Typical blocking status | Expected remediation |
| --- | --- | --- | --- |
| `INSUFFICIENT_EVIDENCE` | Business evidence exists but is not sufficient for the requested assertion or semantic use. | Blocking when the assertion is required for compilation. | Provide additional evidence, record a new source clarification as `SourceArtifact` and `EvidenceFragment`, reduce compilation scope, reject or defer the unsupported assertion, establish not-applicability through evidence or an applicable rule and recalculate the context, or leave the assertion unresolved. |
| `EVIDENCE_REQUIRED` | An accepted source-derived assertion lacks evidence. | Blocking. | Provide evidence or remove the assertion from accepted status. |
| `MISSING_REQUIRED_INFORMATION` | A value is applicable and required but absent, regardless of whether absence is known or unknown. | Blocking. | Provide the required evidence-backed value, establish not-applicability through evidence or an applicable rule and recalculate the context, reduce the requested scope, or defer or reject the unsupported assertion. |
| `UNRESOLVED_INTERPRETATION` | A raw value, statement, label, or source fragment is present, but its business meaning cannot currently be determined. | Blocking when interpretation is required for compilation; non-blocking when retained only as provenance and outside scope. | Obtain source clarification, provide a terminology definition, link an authoritative glossary or policy, record new evidence, or exclude or defer the affected scope. |
| `AMBIGUOUS_BUSINESS_MEANING` | At least two plausible business interpretations exist. | Blocking when the meaning affects compilation. | Provide new evidence, record an authorized `AnalystDecision`, exclude scope, or defer. |
| `CONTRADICTORY_SEQUENCE` | Supported statements imply incompatible ordering. | Blocking. | Resolve by authorized `AnalystDecision` between evidence-backed alternatives, source correction, or scoped exclusion. |
| `CONTRADICTORY_RESPONSIBILITY` | Supported statements assign incompatible responsibility. | Blocking when responsibility is required. | Clarify accountable or performing role through evidence and authorized `AnalystDecision` where needed. |
| `AMBIGUOUS_GATEWAY_SEMANTICS` | Branching or merging business semantics are underdetermined. | Blocking. | Clarify exclusivity, inclusivity, parallelism, default paths, and conditions through evidence or authorized `AnalystDecision`. |
| `EQUIVALENT_BPMN_REPRESENTATIONS` | Business meaning is accepted, but more than one semantically equivalent BPMN representation is available. | Blocking for the affected mapping until policy exists. | Provide `ModelingDecision`, approved mapping policy, or approved BPMN profile. |
| `UNRESOLVED_OPTIONALITY` | Applicability or requirement state is conditional or undetermined without enough condition information. | Usually blocking. | Clarify mandatory, optional, conditional, or not-applicable status through evidence, applicable rule, or authorized `AnalystDecision`. |
| `UNRESOLVED_BUSINESS_CARDINALITY` | Number, multiplicity, or activation count is a business fact and remains unresolved. | Usually blocking. | Provide evidence, authorized `AnalystDecision`, exclusion, or deferral. |
| `MODELING_MULTIPLICITY_POLICY_REQUIRED` | Business cardinality is accepted, but its BPMN representation requires a modeling-policy choice. | Blocking for the affected mapping. | Provide `ModelingDecision` or approved mapping policy. |
| `UNRESOLVED_EVENT_TRIGGER` | Event trigger semantics are not determined. | Blocking when an event mapping is requested. | Provide trigger evidence, record an authorized `AnalystDecision` between evidence-backed interpretations, or exclude or defer the affected scope. A different mapping may be selected only when it preserves already accepted event semantics and does not bypass the unresolved trigger. |
| `UNRESOLVED_PARTICIPANT_IDENTITY` | The business participant, organization, responsibility boundary, or interaction boundary is not determined. | Blocking when participant meaning affects compilation or BPMN legality. | Provide evidence or authorized `AnalystDecision`. |
| `PARTICIPANT_REPRESENTATION_POLICY_REQUIRED` | Participant meaning is accepted, but representing it as pool, lane, black-box participant, or another allowed construct requires modeling policy. | Blocking for the affected representation. | Provide `ModelingDecision`, target profile, or mapping policy. |
| `SEMANTIC_CONTEXT_REQUIRED` | A context-sensitive record lacks an explicit or inherited semantic context. | Blocking when the record affects compilation. | Add explicit `context_ref` or define package-level default context with traceable inheritance. |
| `SEMANTIC_CONTEXT_MISMATCH` | Records required for one compilation scope refer to incompatible contexts, versions, perspectives, variants, organizational scopes, or effective periods. | Blocking. | Align contexts, split the compilation request, obtain a scoped analyst decision, or exclude incompatible records. |
| `DECISION_AUTHORITY_REQUIRED` | An authoritative `AnalystDecision` lacks a valid `DecisionAuthorityRef`. | Blocking. | Provide a valid authority reference or treat the decision as non-authoritative. |
| `DECISION_AUTHORITY_SCOPE_MISMATCH` | The authority reference does not cover the decision context, category, process, version, organization, or effective time. | Blocking. | Provide a valid scoped authority reference, constrain the decision, or obtain an authorized decision. |
| `UNRESOLVED_REFERENCE` | A referenced record cannot be resolved. | Blocking. | Correct reference, restore record, or remove dependent mapping. |
| `UNSUPPORTED_MAPPING` | Requested mapping is outside current compiler capability or policy. | Blocking for that mapping. | Add support later or select a supported mapping through review. |
| `MAPPING_NOT_ELIGIBLE` | A mapping proposal does not satisfy compiler eligibility conditions. | Blocking for that mapping. | Resolve missing facts, references, blocking findings, context mismatch, authority gaps, or target-profile mismatch. |
| `MODELING_POLICY_REQUIRED` | Accepted semantic meaning exists, but semantic compilation requires a missing modeling policy or profile. | Blocking for the affected compilation or mapping; not evidence-related and not proof of unresolved business meaning. | Provide or approve the required `CompilationPolicyContext`, add an applicable `ModelingDecision`, select an approved modeling profile, or restrict the requested compilation scope. |
| `TARGET_BPMN_PROFILE_REQUIRED` | Compilation eligibility or kernel validation requires a declared target BPMN profile, but none is available. | Blocking. | Provide a `target_bpmn_profile` in `CompilationPolicyContext` and propagate it through compilation and validation. |
| `TARGET_BPMN_PROFILE_MISMATCH` | Pipeline artifacts or mappings reference incompatible target BPMN profiles. | Blocking. | Align profiles, record a compatible profile transformation, or split the compilation request. |
| `PARTIAL_COMPILATION_POLICY_REQUIRED` | Partial compilation was requested or implied without explicit policy enablement. | Blocking for partial output. | Explicitly enable partial compilation in `CompilationPolicyContext` or refuse the full requested scope. |
| `PARTIAL_COMPILATION_DEPENDENCY_BLOCKED` | A proposed partial fragment depends on unresolved or incompatible records outside the fragment. | Blocking for that fragment. | Resolve dependencies, expand the fragment scope, or exclude the fragment. |
| `HUMAN_DECISION_REQUIRED` | Contract requires human authority before compilation may proceed. | Blocking. | Record an evidence-aware `AnalystDecision` with valid `DecisionAuthorityRef`. |
| `STALE_ANALYST_DECISION` | A decision refers to superseded evidence, records, authority, context, or process version without review. | Blocking when the decision is material. | Reconfirm, supersede, reject, or constrain the decision. |
| `PROVENANCE_MISSING` | Required provenance is absent. | Blocking. | Attach evidence, decision, context, or mapping-rule references. |
| `UNAUTHORIZED_ACCEPTANCE` | A record was marked accepted without valid human authority in M1. | Blocking. | Revert status or add a valid `AnalystDecision` with valid `DecisionAuthorityRef`. |
| `RECOMMENDATION_NOT_AUTHORITY` | A recommended decision was used as if it were authoritative. | Blocking. | Add human analyst decision or keep the issue unresolved. |
| `CONFIDENCE_ONLY_RECOMMENDATION` | A material recommendation selected an alternative using confidence as its sole differentiator. | Blocking for use of that recommendation. | Add a non-confidence rationale or return `no-recommendation`. |
| `PROPOSED_RECORD_NOT_AUTHORITATIVE` | Proposed meaning was used for authoritative compilation. | Blocking. | Obtain human acceptance or restrict processing to diagnostics and planning. |
| `INVALID_VALUE_STATE_COMBINATION` | The selected knowledge, applicability, requirement, and presence dimensions are internally inconsistent, excluding explicitly valid known-absence combinations. | Blocking when the value affects compilation. | Correct the dimension values or record an explicit historical/provenance exception. |

Business-semantic diagnostics require evidence, source clarification, an authorized `AnalystDecision`, scope exclusion, or deferral.

Modeling-policy diagnostics may require a `ModelingDecision`, mapping policy, modeling profile, compiler policy, or a selection among semantically equivalent representations.

A modeling policy MUST NOT resolve a business-semantic diagnostic. `CompilationPolicyContext` MAY resolve only modeling-policy diagnostics. It MUST NOT resolve business-semantic diagnostics.

`MODELING_POLICY_REQUIRED`, `EQUIVALENT_BPMN_REPRESENTATIONS`, `MODELING_MULTIPLICITY_POLICY_REQUIRED`, and `PARTICIPANT_REPRESENTATION_POLICY_REQUIRED` MUST NOT be used when business evidence is missing. `INSUFFICIENT_EVIDENCE`, `AMBIGUOUS_BUSINESS_MEANING`, `UNRESOLVED_BUSINESS_CARDINALITY`, `UNRESOLVED_EVENT_TRIGGER`, and `UNRESOLVED_PARTICIPANT_IDENTITY` MUST NOT be used when the business meaning is accepted but a compiler policy is missing.

A modeling policy may determine how unresolved or excluded content is represented, but it cannot make insufficient business evidence sufficient.

A modeling or mapping choice MUST NOT bypass unresolved event-trigger business semantics. `CompilationPolicyContext` and `ModelingDecision` cannot resolve an unresolved business event trigger.

## 17. Compilation outcomes and partial-compilation policy

Partial compilation is disabled by default.

M1 conceptually defines `partial_compilation_mode` as either disabled or enabled. This is not a machine enum.

When partial compilation is disabled and any blocking diagnostic affects the requested compilation scope:

- authoritative compilation of the requested scope is refused,
- no partial result may be presented as completion.

When partial compilation is enabled, it MAY occur only when explicitly enabled by `CompilationPolicyContext`.

The compiler MAY produce an authoritative fragment only when:

- the fragment uses accepted semantics,
- the fragment is evidence-backed,
- all fragment references resolve,
- its dependency closure contains no blocking diagnostic,
- it belongs to one compatible `SemanticContext`,
- it is eligible under the target BPMN profile,
- unresolved scope is explicitly excluded.

`CompilationResult` MUST distinguish:

- `requested_scope`,
- `authoritative_compiled_scope`,
- `non_authoritative_scope`,
- `excluded_scope`,
- `unresolved_scope`.

A fragment in `authoritative_compiled_scope` remains authoritative only for that explicit scope. Overall outcome `partially-compiled` MUST NOT be presented as a complete process model. Unresolved scope MUST remain visible. Excluded scope MUST include reasons and diagnostics. Partial compilation MUST NOT hide cross-fragment dependencies.

`compiled`: all required semantics for the requested scope were compiled without blocking diagnostics.

`partially-compiled`: explicitly permitted independent fragments were compiled, but the overall requested scope remains incomplete and blocking diagnostics remain outside the authoritative compiled scope.

`refused`: no authoritative result was produced because required semantics were unresolved or unsupported.

`partially-compiled` MUST NOT be presented as a completed BPMN model. `refused` is a valid contract outcome. A technically successful serialization is not equivalent to semantic compilation success.

## 18. Versioning

The Process IR MUST include an explicit `ir_version`. Backward-compatibility rules MUST be defined before machine serialization. Unsupported major versions MUST be rejected or migrated through an explicit process. Unknown extension data SHOULD be preserved where possible.

M1 does not choose JSON Schema, protobuf, database representation, programming-language representation, or transport protocol. Serialization technology is a later decision.

## 19. Synthetic example

This compact example is fictional. It does not use real company names, personal names, internal URLs, proprietary document wording, or confidential source material.

### Source evidence

- `EF-001`: "A budget review is required for every sourcing request."
- `EF-002`: "A security review is required only when the checklist indicates security impact."
- `EF-003`: "Required reviews begin at the same time after the request is prepared."
- `EF-004`: "Managerial approval is completed before financial control."
- `EF-005`: "Financial control is completed before managerial approval."

### Semantic context and target profile

`CTX-001` is the explicit `SemanticContext` for the current AS-IS process version and modeled sourcing fragment.

`PROFILE-001` is the declared `target_bpmn_profile` for the compilation request. The example does not define the profile registry.

### Atomic statements

- `ST-001`: budget review is always required, supported by `EF-001`.
- `ST-002`: security review is conditional, supported by `EF-002`.
- `ST-003`: review activities may begin concurrently, supported by `EF-003`.
- `ST-004`: managerial approval precedes financial control, supported by `EF-004`, confidence 0.72.
- `ST-005`: financial control precedes managerial approval, supported by `EF-005`, confidence 0.86.

### Candidate entities

- `CE-BUDGET-REVIEW`: activity candidate, proposed name "Budget review", supported by `ST-001`.
- `CE-SECURITY-REVIEW`: activity candidate, proposed name "Security review", supported by `ST-002`.
- `CE-MANAGER-APPROVAL`: activity candidate, proposed name "Managerial approval", supported by `ST-004` and `ST-005`.
- `CE-FINANCIAL-CONTROL`: activity candidate, proposed name "Financial control", supported by `ST-004` and `ST-005`.

### Candidate relations

- `CR-BUDGET-ALWAYS`: `CE-BUDGET-REVIEW` is mandatory, supported by `ST-001`.
- `CR-SECURITY-CONDITIONAL`: `CE-SECURITY-REVIEW` is conditional-on checklist security impact, supported by `ST-002`.
- `CR-REVIEWS-CONCURRENT`: `CE-BUDGET-REVIEW` is parallel-with `CE-SECURITY-REVIEW` when both are active, supported by `ST-003`.
- `CR-MANAGER-BEFORE-FINANCE`: `CE-MANAGER-APPROVAL` precedes `CE-FINANCIAL-CONTROL`, supported by `ST-004`.
- `CR-FINANCE-BEFORE-MANAGER`: `CE-FINANCIAL-CONTROL` precedes `CE-MANAGER-APPROVAL`, supported by `ST-005`.

### Finding and unresolved question

`FIND-SEQ-001` is a contradiction finding affecting `CR-MANAGER-BEFORE-FINANCE` and `CR-FINANCE-BEFORE-MANAGER`. It is blocking because the ordering is required for authoritative compilation of that fragment.

`Q-SEQ-001` asks: "Does managerial approval occur before or after financial control for the current process version?"

### Alternative BPMN mapping proposals

- `MAP-REVIEWS-001`: proposed inclusive gateway or equivalent pattern for mandatory budget review plus conditional security review.
- `MAP-SEQ-001A`: proposed sequence flow from managerial approval to financial control.
- `MAP-SEQ-001B`: proposed sequence flow from financial control to managerial approval.

These mappings are non-authoritative proposals. `MAP-SEQ-001A` and `MAP-SEQ-001B` cannot both be eligible for the same process scope.

### RecommendedDecision outcome

`REC-SEQ-001` records `recommendation_outcome = no-recommendation`.

The rationale states that no non-confidence criterion distinguishes the alternatives. `ST-005` has higher confidence than `ST-004`, but confidence alone is not authority and is not sufficient rationale for selecting `MAP-SEQ-001B`.

`REC-SEQ-001` preserves both alternatives, leaves `FIND-SEQ-001` unresolved, does not unblock compilation, and does not change any record to `accepted`.

### A. Before analyst decision

Before an `AnalystDecision` exists:

- both contradictory sequence interpretations remain preserved,
- confidence values may differ,
- the agent does not recommend one solely because its confidence is higher,
- the recommendation outcome is `no-recommendation`,
- the rationale states that no non-confidence criterion distinguishes the alternatives,
- the Semantic Compiler returns `refused`,
- diagnostics include `CONTRADICTORY_SEQUENCE`,
- diagnostics include `HUMAN_DECISION_REQUIRED`,
- no gateway or sequence is selected for the contradiction.

### B. After analyst decision

After human review, `AUTH-001` records a `DecisionAuthorityRef` for a human actor authorized for sequencing decisions in `CTX-001`.

`AD-SEQ-001` records an `AnalystDecision` with `decision_outcome = resolve`, `context_ref = CTX-001`, and authority reference `AUTH-001`. It selects `CR-FINANCE-BEFORE-MANAGER` for the current process version and rejects `CR-MANAGER-BEFORE-FINANCE` for that scope.

After `AD-SEQ-001`:

- the selected interpretation becomes accepted for compilation,
- the rejected interpretation remains preserved in provenance,
- the contradiction remains historically traceable,
- compilation may proceed only for the resolved scope,
- any produced `CompiledSemanticModel` must reference `CTX-001` and `PROFILE-001`,
- downstream BPMN validation remains required.

### Manual review tests

Question: If the higher-confidence interpretation were removed, would compiler behavior before the `AnalystDecision` change?

Expected answer: No. Authoritative compilation remains refused until an explicit human `AnalystDecision` or sufficient new evidence resolves the contradiction.

Question: If the confidence values of the two contradictory statements were exchanged, would the compiler or recommendation outcome before the `AnalystDecision` change?

Expected answer: No. The compiler remains refused and the agent remains at `no-recommendation` unless a non-confidence criterion or new evidence resolves the contradiction.

The example fails semantic acceptance if changing confidence alone changes the authoritative compilation outcome, the selected sequence, or the recommendation from `no-recommendation` to a preferred alternative.

## 20. Open decisions

The following implementation decisions remain intentionally outside M1:

- serialization format,
- exact identifier syntax,
- timestamp representation,
- analyst identity representation,
- confidence calibration,
- extension mechanism,
- persistence,
- transport API,
- common immutable `RecordEnvelope`,
- deterministic replay metadata and digests,
- diagnostic severity and aggregation rules,
- decision staleness and invalidation rules,
- detailed mapping-rule versioning,
- machine-readable schema,
- expanded executable contract-test matrix.

Partial-compilation policy is no longer entirely open in M1. The default is disabled, and enablement requires explicit `CompilationPolicyContext`. Detailed future serialization, dependency-closure algorithms, replay metadata, and executable validation remain outside M1.

The following are not open in M1:

- human decision authority in M1,
- the distinction between evidence and confidence,
- the distinction between recommendation and `AnalystDecision`,
- the prohibition on agent-declared BPMN validity,
- the four value-state dimensions defined by this contract,
- the placement of `ModelingDecision` in `CompilationPolicyContext`,
- the requirement for `SemanticContext` on context-sensitive records,
- the requirement for `DecisionAuthorityRef` on authoritative `AnalystDecision` records,
- the separation of `CompiledSemanticModel` from `CompilationResult`,
- the requirement to propagate `target_bpmn_profile`.

## 21. Acceptance model

### 21.1 Author self-check

The author may verify only:

- all required sections exist,
- required terms are defined,
- required diagnostics are included,
- requirement language is used consistently,
- the synthetic example contains both required states,
- Markdown renders correctly,
- no prohibited implementation artifacts were created.

Passing the author self-check does not constitute semantic acceptance.

### 21.2 Human semantic acceptance

Human review MUST evaluate:

- whether the Agent-Compiler boundary is enforceable,
- whether any clause allows the agent to smuggle an authoritative decision,
- whether the compiler can reinterpret or invent business meaning,
- whether refusal behavior is explicit and complete,
- whether known-absence semantics are correct,
- whether the four-axis value model is semantically sound,
- whether the validity and compatibility rules for four-axis combinations are sufficient,
- whether `ProcessIRPackage` and `CompilationResult` are separated correctly,
- whether evidence and decision authority are separated correctly,
- whether evidence diagnostics and modeling-policy diagnostics are separated correctly,
- whether mapping eligibility authority belongs to the Semantic Compiler as stated,
- whether `CompilationPolicyContext` is limited to semantic compilation policy,
- whether the downstream rendering-policy boundary is sufficient,
- whether `UNRESOLVED_INTERPRETATION` correctly distinguishes unknown interpretation from ambiguity,
- whether `RecommendedDecision` and `AnalystDecision` are sufficiently distinct,
- whether the selected `no-recommendation` representation is acceptable,
- whether the placement of `ModelingDecision` in `CompilationPolicyContext` is acceptable,
- whether accepted business meaning is clearly separated from BPMN validity,
- whether the revised synthetic example truly preserves uncertainty before human decision,
- whether `SemanticContext` makes contextual terms enforceable,
- whether `DecisionAuthorityRef` adequately defines authorization semantics without implementation details,
- whether `CompiledSemanticModel` is separated from `CompilationResult`,
- whether business-semantic diagnostics are separated from modeling-policy diagnostics,
- whether the partial-compilation policy is strict enough,
- whether `AnalystDecision.decision_outcome` covers required outcomes without creating modeling decisions,
- whether `target_bpmn_profile` propagation is sufficient,
- whether the required-versus-not-applicable rule is consistent,
- whether any compiler-policy boundary remains ambiguous.

Final human semantic review is complete. Semantic acceptance is granted by the project decision authority issuing the final M1 corrections, acceptance, merge, and project-memory synchronization instruction. The accepted scope is the conceptual M1 Process IR contract. Machine-readiness and implementation work remain deferred to M1.2 and M2.

## 22. Acceptance criteria

The document is semantically accepted for M1 on the basis that it:

- defines the Agent-Compiler boundary,
- distinguishes evidence, statements, candidates, mappings, findings, recommendations, decisions, modeling decisions, and diagnostics,
- distinguishes recommendation from human decision authority,
- defines `recommended_decisions` in the package envelope,
- prevents confidence-only recommendations,
- defines `no-recommendation`,
- replaces the single knowledge-state enum with four independent dimensions,
- defines compatibility constraints for dimension combinations,
- explicitly supports known absence,
- treats missing required information as a derived condition, not a knowledge state,
- defines `SemanticContext`,
- requires `context_ref` for context-sensitive records,
- defines `DecisionAuthorityRef`,
- requires valid decision authority for authoritative `AnalystDecision` records,
- defines `CompiledSemanticModel`,
- separates `ProcessIRPackage`, `CompiledSemanticModel`, `CompilationResult`, and `KernelValidationReport`,
- defines proposed records as inspectable but not authoritatively compilable,
- assigns mapping eligibility to the Semantic Compiler,
- requires evidence for accepted source-derived assertions,
- prevents `AnalystDecision` from replacing evidence,
- prevents `ModelingDecision` from remediating insufficient business evidence,
- separates business-semantic diagnostics from modeling-policy diagnostics,
- defines explicit partial-compilation default and enablement behavior,
- defines `AnalystDecision.decision_outcome`,
- propagates `target_bpmn_profile` across compilation and validation,
- corrects required versus not-applicable semantics,
- separates `CompilationPolicyContext` from downstream rendering policy,
- defines `UNRESOLVED_INTERPRETATION`,
- explicitly places `ModelingDecision`,
- contains one synthetic end-to-end example with before and after states,
- includes both manual review tests,
- makes no implementation or conformance claims,
- records final human semantic acceptance.

This document is semantically accepted for M1. It MUST NOT be described as machine-schema-ready, implementation-complete, production-ready, or proof that any specific process model is BPMN-valid.
