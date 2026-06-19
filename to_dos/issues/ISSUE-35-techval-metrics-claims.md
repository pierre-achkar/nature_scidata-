# ISSUE-35: Define extraction-validation claims and metrics

## What to do

- Define exactly what the extraction validation will measure.
- State the primary validation units, metrics, and uncertainty reporting.
- Keep the primary emphasis on extraction correctness for the parsed-full-text subset of roughly 60k reviews.

## How to do it

- Decide whether validation is reported at the field-instance level, review level, or both.
- Define the main correctness metrics for extracted non-null values and the main coverage or abstention statistics.
- Decide which confidence intervals or uncertainty summaries will be reported.
- Ensure the chosen metrics can be paired with a statistically justified sample size.
- Document the design in `SCIDATA_26_SR4ALL/scidata--sr4all-part4.tex`.

## Definition of done

- The manuscript states what constitutes a validation item.
- The manuscript states which metrics are reported and why they support the paper's claims.
- The validation plan includes uncertainty reporting rather than point estimates only.
