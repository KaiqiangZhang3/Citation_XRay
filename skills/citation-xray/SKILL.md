---
name: citation-xray
description: Build audit-ready citation-level datasets from legal, academic, and policy documents. Use when a user wants to process PDFs, chapters, articles, commentaries, reports, or footnotes into structured data by locating argument-relevant passages, mapping footnotes, splitting independent sources, resolving ibid/supra/see-note cross-references, classifying citation function, source type, origin/jurisdiction, and uncertain items. Do not use merely to summarize a document or to generate final charts/statistics without first building the underlying dataset.
---

# Citation X-Ray & Source Classification Skill

## Purpose

This skill turns dense legal, academic, or policy documents into **audit-ready citation-level datasets**.

It is a backend-style workflow. Its primary job is to create reliable underlying data:

- argument-relevant paragraphs
- paragraph-to-footnote mappings
- independent source splits
- cross-reference resolution
- citation function judgments
- source type classifications
- origin / jurisdiction classifications
- uncertain and excluded items

Downstream outputs such as statistics, dashboards, pie charts, citation networks, written explanations, or article drafts are optional and should be generated only after the dataset is created.

## When to use

Use this skill when the user asks to:

- “拆文件”, “拆脚注”, “拆引文”, “做 citation x-ray”
- analyze footnotes, sources, citations, references, or authority structure
- classify sources into scholar writings, state practice, UN documents, treaties, cases, etc.
- compare citation structure across versions, chapters, articles, or years
- build a structured citation dataset for later visualization/statistics/dashboard use
- audit AI-generated citation statistics or correct misclassified sources
- extract a source-level dataset from legal commentaries, treaty commentaries, law review articles, books, government reports, or international law materials

## When not to use

Do not use this skill when the user only wants:

- a simple summary
- translation
- general legal explanation without citation-level data
- a final pie chart/table without an auditable source dataset
- a conclusion about the document without inspecting the underlying footnotes

## Core principle

Do not start with statistics. Start with the evidence trail.

The workflow is:

1. locate argument-relevant passages
2. map their footnotes
3. split independent sources
4. resolve cross-references
5. classify citation function
6. classify source type
7. classify origin / jurisdiction
8. list uncertain and excluded items
9. optionally generate final outputs

## Hard rules

1. Do **not** count a whole footnote as one source when it contains multiple sources.
2. Do **not** count `ibid.`, `supra`, `see n.`, `see MN`, `see Art.`, or internal cross-references as new sources.
3. Resolve cross-references to their underlying external sources. If already counted, mark duplicate and do not count again.
4. Do **not** classify a scholarly work about a treaty as a treaty/formal instrument.
5. Do **not** classify article-by-article commentaries as treaties or official documents merely because they discuss a treaty/charter provision.
6. Do **not** count contrary views, reservations, or “still applicable” positions as support for an “obsolete/no longer applicable” argument.
7. Watch for signal phrases: `but see`, `however`, `on the other hand`, `critically`, `contrary view`, `unconvincing position`, `retain full significance`, `still applicable`, `not affected`.
8. Do not force-classify uncertain items. `uncertain` is a valid audit result.
9. Always keep enough source text to let a human verify the judgment.
10. Final statistics are optional and should state their counting rule.

## Required inputs

If not provided, ask the user for the missing critical items.

- documents to process
- target argument or research question
- counting unit: citation occurrence, unique source, or both
- support-scope: narrow direct support only, or broad support including auxiliary paths
- source-type taxonomy
- origin/jurisdiction taxonomy
- whether to deduplicate repeated citations across articles/chapters/years
- desired output format: Markdown, CSV, JSON, or database-ready tables

## Default taxonomies

### Citation function

Use these labels:

- core_support
- auxiliary_support
- historical_background
- contrary_or_reserved_view
- neutral_context
- internal_cross_reference
- duplicate_already_counted
- uncertain

Only `core_support` and `auxiliary_support` are countable by default.

### Source type

Use these labels:

- scholarly_writing
- government_or_state_practice
- international_organization_document
- treaty_or_formal_instrument
- case_or_judicial_material
- bibliography_only
- internal_cross_reference
- other
- uncertain

### Origin / jurisdiction

Use a project-specific taxonomy when supplied. Otherwise use:

- Germany / German-language legal tradition
- Japan
- France / French commentary tradition
- United Nations / international organization
- other state / other country
- mixed
- uncertain

When classifying by legal tradition instead of strict nationality, state the rule explicitly.

## Standard workflow

### Step 1 — Document intake

Create a document metadata table.

Fields: document_id, file_name, title, year, edition/version, chapter/article/section, page range, paragraph/MN range, text quality, footnote quality, OCR needed?, notes.

### Step 2 — Argument paragraph locator

Find only passages relevant to the user’s target argument.

Fields: paragraph_id, document_id, year, article/chapter, page, MN/paragraph number, passage excerpt, target keywords, argument pathway, enter_next_step?, reason.

Do not process the whole document unless the user asks for full-document coverage.

### Step 3 — Footnote mapper

For each relevant passage, map the footnotes attached to that passage.

Fields: footnote_id, paragraph_id, document_id, page/MN, footnote_number, footnote_text, footnote_complete?, needs_cross_reference_resolution?, notes.

### Step 4 — Independent source splitter

Split each footnote into independent sources.

Fields: source_item_id, footnote_id, source_sequence, original_source_text, normalized_short_label, appears_to_be_external_source?, needs_cross_reference_resolution?, split_confidence, notes.

### Step 5 — Cross-reference resolver

Resolve ibid/supra/note/MN/article references.

Fields: cross_ref_id, source_item_id, original_reference, reference_type, target_location, resolved_source_text, resolved_source_item_id if known, already_counted?, count_decision, notes.

### Step 6 — Citation function classifier

Classify what each source does in the argument.

Fields: source_item_id, citation_function, countable_for_target_argument?, reason, signal_words, context_excerpt, confidence.

### Step 7 — Source type classifier

Classify the document type.

Fields: source_item_id, source_type, type_reason, type_confidence, possible_alternative_type.

### Step 8 — Origin classifier

Classify origin / jurisdiction / legal tradition.

Fields: source_item_id, origin_class, origin_reason, origin_confidence, strict_nationality_or_legal_tradition?, mixed_origin_note.

### Step 9 — Uncertain and excluded audit

Create a separate audit table.

Fields: item_id, location, original_text, issue_type, why_uncertain_or_excluded, what_evidence_is_needed, recommended_action, affects_statistics?.

### Step 10 — Optional downstream outputs

Only after the dataset is complete or the user explicitly asks: count tables, percentages, charts, dashboards, citation networks, written explanation, errata report.

Always state counting unit, support scope, exclusions, uncertain items, and deduplication rule.

## Required behavior during use

When running this skill, prefer producing the base dataset first. If the user asks for final statistics too early, warn that the numbers are provisional unless the audit tables have been reviewed.

When the user provides an errata file, apply only the corrections the user accepted. Do not reintroduce rejected recommendations.

When source classification is unclear, mark `uncertain` rather than guessing.

## Bundled references

Load only the reference files needed for the user's task:

- `references/WORKFLOW.md` when planning or running the full citation pipeline.
- `references/RULES.md` when deciding countability, source type, origin, or cross-reference treatment.
- `references/SCHEMAS.md` when producing Markdown, CSV, JSON, or database-ready tables.
- `references/PROMPTS.md` when the user wants reusable prompts or a staged workflow handoff.
- `references/KNOWN_ERROR_PATTERNS.md` when auditing outputs or correcting likely misclassifications.
