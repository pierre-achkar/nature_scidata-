# ISSUE-03: Explain how corpus layers link together

## What to do

- Explain how OpenAlex metadata, references, and extracted method fields relate to each other.
- Clarify which layers exist for all reviews and which exist only for subsets.

## How to do it

- Map the dataset into layers and state the join keys explicitly.
- Describe which fields depend on full-text availability.
- Treat normalized-query detail as secondary here; reserve concrete query-normalization examples for `Usage Notes`.
- Add this explanation to `SCIDATA_26_SR4ALL/scidata--sr4all-part3.tex`.

## Definition of done

- `Data Records` explains cross-layer linkage clearly.
- The subset logic is explicit.
- A reader can tell how to reconstruct a review-level record across layers.
