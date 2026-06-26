# Modular Prompts

## Prompt 0 — Master rules

You are processing legal/academic documents into an auditable citation-level dataset. Do not produce final statistics first. Follow the pipeline: locate target-argument passages; map footnotes; split independent sources; resolve cross-references; classify citation function; classify source type; classify origin; list uncertain/excluded items; generate optional outputs only after the dataset is built.

Rules: Do not count cross-references as sources. Do not count contrary/reserved views as support. Do not treat scholarly works about treaties as treaty texts. Do not force-classify uncertain items. Preserve original source text for audit. For scanned or low-quality PDFs, complete extraction QC and human correction or explicit provisional acceptance before classification.

## Prompt 0A — PDF extraction QC

For each PDF, detect text-layer status, OCR need, OCR engine if used, page-level confidence if available, footnote number range, missing numbers, duplicate numbers, possible merged notes, embedded note numbers, low-confidence notes, incomplete notes, and unresolved cross-references. Save human-readable review materials separately from CSV/JSON data. Do not classify source function/type/origin until extraction is reviewed or explicitly accepted as provisional.

## Prompt 1 — Argument locator

Read the provided documents. Locate passages relevant to the following target argument: [INSERT TARGET ARGUMENT].

Output: paragraph_id, document_id, year, article/chapter, page, MN/paragraph, excerpt, keywords, argument_pathway, enter_next_step, reason.

Argument pathway labels: direct_argument, auxiliary_argument, institutional_reform_context, background_only, contrary_or_reserved_view, uncertain.

## Prompt 2 — Footnote mapper

For each passage marked enter_next_step=yes, extract the corresponding footnotes. Output footnote_id, paragraph_id, page/MN, footnote_number, footnote_text, complete, needs_resolution, notes.

## Prompt 3 — Source splitter

Split each footnote into independent source items. Output source_item_id, footnote_id, sequence, original_source_text, normalized_label, external_source, needs_resolution, notes.

## Prompt 4 — Cross-reference resolver

Resolve all ibid/supra/note/MN/article references. Output cross_ref_id, source_item_id, original_reference, reference_type, target_location, resolved_source_text, already_counted, count_decision, notes.

## Prompt 5 — Citation function classifier

For each source item, classify its function in relation to the target argument. Labels: core_support, auxiliary_support, historical_background, contrary_or_reserved_view, neutral_context, internal_cross_reference, duplicate_already_counted, uncertain.

## Prompt 6 — Source type classifier

Classify each countable source by type: scholarly_writing, government_or_state_practice, international_organization_document, treaty_or_formal_instrument, case_or_judicial_material, bibliography_only, internal_cross_reference, other, uncertain.

## Prompt 7 — Origin classifier

Classify each countable source by origin/jurisdiction/legal tradition. Use the project taxonomy or default categories: Germany/German-language legal tradition, Japan, France/French commentary tradition, United Nations/international organization, other state/country, mixed, uncertain.

## Prompt 8 — Uncertain audit

List all uncertain and excluded items with item_id, location, original_text, issue_type, extraction_stage, why_uncertain_or_excluded, verification_steps_taken, evidence_checked, evidence_needed, confidence_basis, recommended_action, affects_statistics. Use precise issue types for OCR, text layer, numbering, split, cross-reference, source identity, source type, origin, citation function, duplicate/deduplication, and excluded non-support issues. Do not hide uncertain items.

## Prompt 9 — Optional statistics

Only after the user confirms the audit table, generate requested downstream outputs such as count tables, percentages, charts, dashboards, citation networks, explanatory prose, or errata reports. Always state counting unit, exclusions, and uncertain rule.
