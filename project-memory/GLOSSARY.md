# Glossary

## Terms

- **MøtiveFōrce**: Human-facing product name for the BPMN Semantic Process Analyst concept.
- **canonical semantic model**: Accepted M0 concept; the authoritative process representation containing evidence, statements, findings, ambiguities, decisions, business relationships, BPMN semantics, and separate diagram information.
- **projection**: Generated output from the canonical model, such as BPMN XML, BPMN DI, draw.io files, tables, RACI matrices, and reports.
- **Analytical Agent**: Component that interprets source material and proposes statements, candidates, findings, questions, and mappings. Merged M0 says it is not the authority for BPMN validity.
- **Process IR**: Accepted M1 contract boundary between Analytical Agent and Semantic Compiler.
- **Semantic Compiler**: Component that maps approved business meaning to BPMN concepts. Detailed M1 rules are accepted in PR #2.
- **BPMN Kernel**: Future deterministic BPMN 2.0.2 validation component. Not implemented.
- **evidence**: Source-backed support for an assertion. M0 treats source evidence as part of the canonical model.
- **finding**: Recorded issue such as ambiguity, contradiction, missing information, or conflict.
- **ambiguity**: A condition where multiple plausible interpretations exist.
- **contradiction**: A condition where materially incompatible claims are supported by available evidence.
- **confidence**: Accepted M1 metadata about extraction or interpretation reliability; not authority and not evidence.
- **RecommendedDecision**: Accepted M1 non-authoritative agent recommendation or `no-recommendation` outcome.
- **AnalystDecision**: Accepted M1 explicit human decision for accepting, rejecting, or resolving business meaning.
- **ModelingDecision**: Accepted M1 compiler-policy decision that does not create a business fact.
- **SemanticContext**: Accepted M1 context record that scopes assertions, value states, findings, decisions, mappings, and compilation requests.
- **DecisionAuthorityRef**: Accepted M1 authority reference explaining why a human actor is authorized to issue an `AnalystDecision` in a given context.
- **CompiledSemanticModel**: Accepted M1 deterministic semantic model produced by the Semantic Compiler and consumed by the BPMN Kernel.
- **CompilationResult**: Accepted M1 Semantic Compiler output separate from `ProcessIRPackage`.
- **KernelValidationReport**: Accepted M1 downstream BPMN Kernel validation artifact.
- **target_bpmn_profile**: Accepted M1 profile reference used to scope mapping eligibility, compiled semantic output, and BPMN Kernel validation.
- **authoritative**: Accepted within the relevant authority boundary, such as merged content, human business decision, compiler mapping eligibility, or kernel validation.
- **proposed**: Draft or candidate content not yet accepted.
- **accepted**: Adopted by merged repository content, accepted decision record, or authorized human decision in a stated context.
- **project memory**: Accepted M1.1 repository-native governance memory under `project-memory/`.
