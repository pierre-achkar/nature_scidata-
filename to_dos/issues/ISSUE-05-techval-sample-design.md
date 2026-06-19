# ISSUE-05: Replace the 60-review idea with a defensible sample design

## What to do

- Replace the small qualitative validation idea with a statistically defensible sampling plan for extraction validation.
- Make the sample size and rationale explicit in relation to the target metrics and uncertainty bounds.
- Treat the relevant population as the extracted full-text subset rather than the full 301,871-review corpus.

## How to do it

- Decide what claim the validation sample should support.
- Choose a sample size using a stated rationale rather than convenience, for example target confidence-interval width or minimum per-stratum support.
- Make explicit why a 60-review sample is insufficient for the target claims over a population of roughly 60k extracted reviews.
- Document the design in `SCIDATA_26_SR4ALL/scidata--sr4all-part4.tex`.

## Definition of done

- The manuscript states the validation sample size and why it was chosen.
- The sample design is defensible for reviewer scrutiny.
- The paper no longer relies on an obviously undersized ad hoc sample of 60 reviews.
