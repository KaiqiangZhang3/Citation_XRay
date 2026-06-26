# Workflow Reference

## 0. Set project scope

Before processing, record these project settings:

| Setting | Options |
|---|---|
| target_argument | user-defined |
| document_scope | one file / several files / editions / articles |
| passage_scope | target argument only / full document |
| counting_unit | citation occurrence / unique source / both |
| support_scope | direct support only / direct + auxiliary |
| cross_reference_rule | resolve and deduplicate / count appearances separately |
| uncertain_rule | exclude by default / include after human approval |
| origin_rule | strict nationality / legal tradition / institutional origin |
| output_root | default `output/citation_xray/` unless user specifies otherwise |
| extraction_stage | raw_ocr / raw_text_layer / normalized / human_corrected / classified |

## 1. Extraction and QC gate

For each PDF, detect whether the document has an embedded text layer or requires OCR.

If the PDF is scanned, low-quality, or citation extraction is uncertain:

1. save raw OCR/text artifacts
2. create a readable footnote review pack
3. create per-document footnote data
4. generate `reports/extraction_qc.md`
5. stop before classification unless the user accepts provisional extraction or supplies corrected footnotes

Keep OCR uncertainty separate from citation-function or source-type uncertainty.

## 2. Locate target passages

Do not begin with all footnotes. Start by finding passages relevant to the user’s research question.

Examples of target-expression families for “obsolete clause” arguments:

- obsolete
- lost practical significance
- no longer applicable
- no longer relevant
- transitional character
- admission of former enemy States to the UN
- loss of enemy State status
- efforts to delete/repeal/remove
- UN reform context

For other projects, derive the equivalent expression families from the user’s target argument.

## 3. Map footnotes to passages

Only map footnotes attached to relevant passages unless the user requests full-document coverage.

Before splitting sources, confirm that footnote extraction is `human_corrected`, `normalized`, or explicitly accepted as provisional.

## 4. Split sources

Split semicolon-separated or sentence-separated citations into independent sources.

A source may be a book, article, chapter, commentary entry, government declaration, treaty, UN document, case, official record, report, or document archive item.

Do not split a single source into multiple parts merely because it has title, edition, pages, or publication details.

## 5. Resolve cross-references

Treat these as pointers, not sources: ibid., id., supra, infra, n./note, see MN, see para., see Art., see above/below, same source as.

Resolve them to their target. Then check whether the underlying source has already been counted.

## 6. Classify function

A source can be countable only if it supports the target argument as core or auxiliary support.

Examples of non-countable functions: historical background, contrary view, reservation, neutral context, bibliography-only listing, duplicate cross-reference, unexplained pointer.

## 7. Classify type

Distinguish what the cited item is, not what it is about.

A book about treaties is a scholarly work. A commentary on a charter article is scholarly writing unless it is an official institutional commentary. A treaty text, UNTS entry, official agreement, or formal declaration is treaty/formal or government/state practice depending on context.

## 8. Classify origin

Use the taxonomy chosen for the project. For mixed authorship, either classify as mixed or classify by dominant legal tradition if the project explicitly uses legal-tradition rules.

State the rule in the dataset metadata.

## 9. Audit

Every uncertain item must say what evidence would resolve it. Do not hide uncertain items.

Distinguish OCR, numbering, split, cross-reference, source-identity, source-type, origin, and citation-function issues.

## 10. Optional outputs

Only after the base extraction, source split, cross-reference resolution, classification, and audit tables are complete, generate optional statistics or visualizations.

State the extraction stage used for any statistics.
