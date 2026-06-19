# ISSUE-09: Add corpus-level descriptive checks

## What to do

- Add sanity-check statistics that support trust in the released corpus and contextualize the extraction-validation results.
- Cover field balance, extraction coverage, abstention patterns, and notable outliers.

## How to do it

- Use current corpus counts and distributions already available or easily derivable.
- Add the strongest descriptive checks to the beginning of `Technical Validation`.
- After the descriptive statistics, add targeted sanity checks on notable outliers rather than interleaving the two.
- Reuse or extend current tables if useful.

## Definition of done

- `Technical Validation` includes corpus-level descriptive checks.
- The section shows more than just pipeline description.
- Outliers, abstentions, and distributional caveats are not hidden.
