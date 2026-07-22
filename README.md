# MøtiveFōrce
# BPMN Semantic Process Analyst

System do analizy dokumentów opisujących procesy biznesowe
i budowania audytowalnych modeli zgodnych z BPMN 2.0.2.

## Problem

Najtrudniejszą częścią modelowania procesu nie jest wygenerowanie
BPMN XML, lecz poprawna interpretacja niejednoznacznego tekstu:

- identyfikacja aktywności, zdarzeń i decyzji,
- ustalenie kolejności i warunków,
- rozpoznanie ról, systemów, wejść i wyjść,
- wykrycie konfliktów i braków,
- zachowanie dowodów źródłowych.

## Główna zasada

Diagram BPMN nie jest źródłem prawdy.

Źródłem prawdy jest kanoniczny model semantyczny procesu wraz z:

- evidence,
- findings,
- decyzjami analitycznymi,
- relacjami biznesowymi,
- pełnym modelem BPMN 2.0.2.

## Architektura

1. Process Workbench
2. Agent analityczny
3. Kompilator semantyczny
4. Deterministyczny BPMN 2.0.2 Kernel
5. Adaptery eksportu:
   - BPMN XML
   - BPMN DI
   - draw.io
   - raporty i tabele
   - ADONIS

Graf wiedzy jest planowaną warstwą governance dla wielu procesów.

## Zakres MVP

Wejście:
- DOCX
- PDF
- Markdown
- notatki warsztatowe

Wyjście:
- rejestr aktywności,
- role i uczestnicy,
- RACI,
- wejścia i wyjścia,
- systemy,
- reguły i warunki,
- evidence pack,
- findings register,
- BPMN 2.0.2 XML,
- diagram draw.io.

## Zasady projektowe

- LLM interpretuje tekst, ale nie jest walidatorem BPMN.
- Kernel BPMN działa deterministycznie.
- Każdy element modelu musi wskazywać dowód źródłowy.
- Informacja nieustalona nie może być zastępowana domysłem.
- Tabele są projekcjami modelu, nie jego źródłem.
- Nieznane extension elements muszą być zachowywane.
- Import i eksport BPMN powinny być bezstratne.

## Źródła normatywne

- BPMN 2.0.2 Specification
- BPMN20.cmof
- BPMNDI.cmof
- DI.cmof
- DC.cmof
- BPMN20.xsd
- BPMNDI.xsd
- DI.xsd
- DC.xsd
- Semantic.xsd

## Dokument referencyjny MVP

Proces „Przygotowanie wkładu IT do Sourcingu”.

Materiał zawiera działania, role, dane, warunki,
elementy oznaczone do usunięcia oraz sprzeczne opisy kolejności,
dlatego stanowi test kompletności warstwy analitycznej.

## Status

Projekt koncepcyjny / pre-MVP.
