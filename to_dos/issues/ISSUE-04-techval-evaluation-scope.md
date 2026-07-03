# ISSUE-04: Define extraction-validation scope for `Technical Validation`

## What to do

- Define what `Technical Validation` is meant to establish about the correctness of extracted methodological fields.
- Separate extraction-quality validation from utility demonstration or retrieval use cases.
- Make clear that the section will begin with corpus-level descriptive statistics, then proceed to extraction validation and outlier-oriented sanity checks.

## Key points for the section

- Start with descriptive statistics for the extracted full-text subset.
- Report how many reviews have parsed full texts and how this subset relates to the full corpus.
- Report field coverage for the extracted methodological fields.
- Separate coverage from correctness: a missing value means the pipeline did not retain a verified extraction, not necessarily that the review lacks the information.
- Define the population for extraction validation as the parsed full-text subset, not the full corpus.
- Define the validation unit clearly, e.g., a field value, grouped field, or review-level extraction.
- Statistically justify the validation sample size; do not rely on the previous 60-review sample.
- Stratify the validation sample by discipline and document length.
- Add extraction-profile strata if useful, e.g., records with many extracted fields, few extracted fields, or difficult field types.
- Use manual review as the primary evidence for correctness.
- Validate whether extracted values are supported by the source full text.
- Record abstentions and unsupported values separately.
- Use staged support from stronger LLM re-extraction and LLM-as-judge checks, but keep these as support rather than the main evidence.
- Add sanity checks for outliers after the descriptive statistics.
- Discuss failure patterns such as OCR errors, weak evidence spans, ambiguous reporting, and difficult field types.
- Keep the section focused on trust in the released extracted data.
- Do not turn the section into a retrieval demonstration or a usage-note example.

## How to do it

- List the extraction-validation questions the paper needs to answer.
- Make explicit which claims concern precision of non-null extracted values, which concern coverage or abstention, and which are out of scope.
- State the intended validation flow: descriptive statistics first, then statistically justified manual validation, then supportive staged model-based checks, and finally failure modes and outliers.
- Align them with Scientific Data expectations and reviewer concerns seen in `SDATA-23-nature-journal`.
- Capture the scope in `SCIDATA_26_SR4ALL/scidata--sr4all-part4.tex`.

## Definition of done

- `Technical Validation` has a clear extraction-validation scope statement.
- Each later validation subsection supports a specific data-quality claim.
- The section no longer reads like a placeholder for future work or a use-case section.
