# Output Schemas

Use Markdown, CSV, JSON, or database-ready tables. Do not omit IDs.

## A. Document metadata table

| document_id | file_name | title | year | edition | article_or_chapter | page_range | text_quality | footnote_quality | notes |
|---|---|---|---|---|---|---|---|---|---|

## B. Argument paragraph table

| paragraph_id | document_id | year | article_or_chapter | page | paragraph_or_MN | excerpt | target_keywords | argument_pathway | enter_next_step | reason |
|---|---|---|---|---|---|---|---|---|---|---|

## C. Footnote mapping table

| footnote_id | paragraph_id | document_id | page_or_MN | footnote_number | footnote_text | complete | needs_resolution | notes |
|---|---|---|---|---|---|---|---|---|

## D. Independent source table

| source_item_id | footnote_id | sequence | original_source_text | normalized_label | external_source | needs_resolution | split_confidence | notes |
|---|---|---|---|---|---|---|---|---|

## E. Cross-reference resolution table

| cross_ref_id | source_item_id | original_reference | reference_type | target_location | resolved_source_text | already_counted | count_decision | notes |
|---|---|---|---|---|---|---|---|---|

## F. Citation function table

| source_item_id | citation_function | countable_for_target | signal_words | context_excerpt | reason | confidence |
|---|---|---|---|---|---|---|

## G. Source classification table

| source_item_id | source_type | origin_class | classification_reason | confidence | alternative_classification |
|---|---|---|---|---|---|

## H. Uncertain / excluded audit table

| item_id | location | original_text | issue_type | why_uncertain_or_excluded | verification_steps_taken | evidence_checked | evidence_needed | confidence_basis | recommended_action | affects_statistics |
|---|---|---|---|---|---|---|---|---|---|---|

## I. Optional statistics table

Only generate after audit review or user request.

| year | category_a_count | category_a_percent | category_b_count | category_b_percent | total_count | counting_rule | exclusions |
|---|---:|---:|---:|---:|---:|---|---|
