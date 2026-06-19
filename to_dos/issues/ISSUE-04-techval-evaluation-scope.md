# ISSUE-04: Define extraction-validation scope for `Technical Validation`

## What to do

- Define what `Technical Validation` is meant to establish about the correctness of extracted methodological fields.
- Separate extraction-quality validation from utility demonstration or retrieval use cases.
- Make clear that the section will begin with corpus-level descriptive statistics, then proceed to extraction validation and outlier-oriented sanity checks.

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
