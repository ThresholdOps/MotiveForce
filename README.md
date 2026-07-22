# MøtiveFōrce

**BPMN Semantic Process Analyst**

MøtiveFōrce is a conceptual project for transforming unstructured process descriptions into an auditable semantic process model.

The GitHub repository and technical identifiers use the ASCII name `MotiveForce`.
The human-facing product name is **MøtiveFōrce**.

## Status

**Concept / pre-MVP**

No application, agent, semantic compiler, BPMN kernel, validator, user interface, or export adapter has been implemented yet.

## Core thesis

A BPMN diagram is a projection, not the source of truth.

The source of truth is a canonical semantic process model containing:

- source evidence,
- extracted and normalized business statements,
- findings and contradictions,
- unresolved ambiguities,
- explicit analytical decisions,
- business relationships,
- the complete BPMN 2.0.2 semantic model,
- diagram interchange information kept separately from process semantics.

Tables, diagrams, BPMN XML, BPMN DI, draw.io files, RACI matrices, and external-tool formats are generated projections of that canonical model.

## Problem

Generating XML is not the primary difficulty.

The difficult part is interpreting incomplete, inconsistent, and ambiguous process documentation:

- identifying activities, events, decisions, roles, systems, inputs, and outputs,
- determining sequence, conditions, optionality, and concurrency,
- distinguishing current, historical, proposed, and deleted content,
- resolving inconsistent terminology,
- preserving the source wording,
- detecting contradictions,
- refusing to invent missing process logic.

The system must be able to state that information is unknown or contradictory instead of completing the model by assumption.

## Target architecture

```text
Process Workbench
        ↓
Analytical Agent
        ↓
Process Intermediate Representation
        ↓
Semantic Compiler
        ↓
Deterministic BPMN 2.0.2 Kernel
        ↓
Export Adapters
```

Process Workbench

A human-review environment for inspecting evidence, extracted candidates, proposed interpretations, findings, contradictions, and unresolved questions.

Analytical Agent

Interprets source documents and proposes:

atomic business statements,
activities,
events,
decisions,
roles,
systems,
business data objects,
responsibilities,
sequencing relations,
conditions,
evidence links,
findings and questions.

The agent is probabilistic. It is not the authority for BPMN validity.

Process Intermediate Representation

The structured contract between the Analytical Agent and the Semantic Compiler.

It must preserve:

original evidence,
normalized interpretation,
confidence,
competing interpretations,
missing information,
contradictions,
unresolved questions,
analyst decisions.

An incomplete Process IR must remain explicitly incomplete. It must not be silently converted into a completed process.

Semantic Compiler

Transforms approved business meaning into BPMN concepts.

It selects BPMN structures only when the available information supports the mapping. When the mapping is underdetermined, it produces a diagnostic or a question instead of guessing.

Deterministic BPMN 2.0.2 Kernel

Represents and validates BPMN 2.0.2 deterministically.

The target capability is complete representation of the BPMN 2.0.2 metamodel, including process semantics and BPMN Diagram Interchange.

No conformance claim is made at the current stage.

Future conformance claims must be backed by explicit automated tests and acceptance criteria.

Export adapters

Planned projections include:

BPMN 2.0.2 XML,
BPMN Diagram Interchange,
draw.io / diagrams.net,
process registers, RACI, evidence, and findings reports,
external modeling-tool formats such as future ADONIS-related outputs.

draw.io is therefore an export and visualization adapter. It is not the semantic model or the analytical engine.

Architectural boundary

The central separation is:

The LLM interprets source material.
The Semantic Compiler maps approved meaning.
The BPMN Kernel validates the resulting BPMN model.

This separation must be enforced through data contracts and APIs, not only through prompts.

The agent must not directly declare a model valid and must not bypass the Semantic Compiler or BPMN Kernel.

Primary design tension

The first unresolved architectural problem is the contract between the Analytical Agent and the Semantic Compiler.

The contract must define how to represent:

an evidence fragment,
an extracted statement,
a normalized entity,
a proposed process element,
a proposed relationship,
confidence,
ambiguity,
contradiction,
competing interpretations,
missing mandatory information,
an analyst decision,
compilation diagnostics.

This contract determines whether the rule “the LLM does not validate BPMN” can be enforced structurally rather than remaining a declaration.

Knowledge graph

A cross-process knowledge graph may later support governance of:

roles,
systems,
business data,
controls,
evidence,
organizational relationships,
dependencies between processes.

The knowledge graph is explicitly outside the initial MVP scope and should be reconsidered after the canonical model and Process IR have been validated.

Reference scenario

The first reference scenario will be a sourcing-related process description containing:

inconsistent sequencing,
mandatory and conditional reviews,
parallel behavior,
historical and deleted elements,
duplicated or inconsistent role names,
incomplete business rules,
unresolved workshop decisions.

The purpose of the scenario is to test analytical discipline and evidence traceability, not merely BPMN XML generation.

Next step

Define the minimal data contract between the Analytical Agent and the Semantic Compiler.

The first contract should cover at least:

source evidence,
atomic statements,
candidate entities,
candidate relationships,
candidate BPMN mappings,
findings,
ambiguities,
contradictions,
analyst decisions,
unresolved questions,
compilation diagnostics.

No BPMN Kernel implementation should begin before this boundary is defined.
