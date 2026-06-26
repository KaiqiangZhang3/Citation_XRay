# Output, OCR, and Review Workflow

Use this reference when processing PDFs, scanned documents, multi-document projects, OCR output, or any workflow that produces files.

## Output root

Write project artifacts under:

```text
output/citation_xray/
```

Separate human-readable review materials from machine data:

```text
output/citation_xray/
  readable/
    per_document/
    summary/
  data/
    per_document/
    merged/
  raw/
  corrected/
  reports/
```

Do not mix readable Markdown, raw OCR, CSV/JSON data, page images, and reports in the same directory.

## Single-document and multi-document layout

For every document, assign a stable `document_id` such as `D001`, `D002`, and a short slug such as `2002_Art53`.

Per-document readable files:

```text
readable/per_document/D001_2002_Art53_footnotes.md
```

Per-document data files:

```text
data/per_document/D001_document_metadata.csv
data/per_document/D001_footnotes.csv
data/per_document/D001_sources.csv
data/per_document/D001_crossrefs.csv
data/per_document/D001_audit.csv
```

Merged project files:

```text
data/merged/documents.csv
data/merged/footnotes_all.csv
data/merged/sources_all.csv
data/merged/crossrefs_all.csv
data/merged/audit_all.csv
readable/summary/all_documents_footnotes_index.md
readable/summary/review_notes.md
```

Use document-scoped filenames for per-document files. Avoid generic names such as `footnotes.csv` in multi-document projects.

## Extraction stages

Always label data with one of these stages:

- `raw_ocr`: uncorrected OCR output.
- `raw_text_layer`: uncorrected text extracted from an embedded PDF text layer.
- `normalized`: cleaned spacing, line breaks, hyphenation, or citation punctuation without human source correction.
- `human_corrected`: reviewed and corrected by a human or explicitly accepted by the user.
- `classified`: split, resolved, and classified dataset built from a stated extraction stage.

Statistics must state which stage they use. Final statistics should not rely on `raw_ocr` or `raw_text_layer` unless the user explicitly accepts provisional results.

## OCR and text-layer handling

For each PDF:

1. Detect whether it has an embedded text layer.
2. If scanned or low-quality, run OCR before citation classification.
3. Save raw OCR/text artifacts under `raw/D001/`.
4. Record OCR engine, version if known, page-level confidence when available, and whether page images were saved.
5. Keep OCR uncertainty separate from citation classification uncertainty.

Suggested raw layout:

```text
raw/D001/
  ocr_pages.json
  raw_text_by_page.txt
  page_images/
```

If OCR confidence is low, or footnote text is visibly corrupted, stop at extraction/QC or mark later classification as provisional.

## Extraction gate

Do not move directly from scanned PDF text to source type, origin, or citation function classification.

Before classification, produce:

1. raw extraction artifacts
2. readable footnote review pack
3. per-document footnote table
4. extraction QC report
5. corrected footnote table or explicit user acceptance of provisional extraction

Only then split sources, resolve cross-references, classify function/type/origin, and generate statistics.

## Human review loop

Use this loop for scanned PDFs, low-confidence extraction, or high-stakes statistics:

1. Automatic extraction
2. Human-readable review pack
3. Extraction QC report
4. Human correction of footnotes or user acceptance of provisional extraction
5. Source splitting from corrected or accepted extraction
6. Cross-reference resolution
7. Source classification
8. Audit table review
9. Final or provisional statistics

Save corrected files under:

```text
corrected/D001_footnotes_corrected.csv
corrected/D001_sources_corrected.csv
```

## Extraction QC

Always produce `reports/extraction_qc.md` when processing PDFs.

Include:

- document list and document IDs
- text-layer status for each PDF
- OCR engine and confidence when applicable
- footnote number range
- missing footnote numbers
- duplicate footnote numbers
- possible merged notes
- possible embedded note numbers
- low OCR confidence notes
- incomplete or truncated notes
- unresolved cross-references
- items blocked from classification pending correction

## Audit issue types

Use precise issue types in audit tables:

- `ocr_issue`
- `text_layer_issue`
- `footnote_numbering_issue`
- `split_issue`
- `cross_reference_issue`
- `source_identity_uncertainty`
- `source_type_uncertainty`
- `origin_uncertainty`
- `citation_function_uncertainty`
- `duplicate_or_deduplication_issue`
- `excluded_non_support`

Do not merge OCR problems with legal or citation-function uncertainty. A corrupted OCR token and an ambiguous source function are different audit issues.
