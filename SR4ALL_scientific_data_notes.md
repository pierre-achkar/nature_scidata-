# SR4ALL Scientific Data plan

## Goal

- Resubmit `Webis-SR4ALL-26` to *Nature Scientific Data* as a `Data Descriptor`.
- Reframe the paper as a dataset paper, not as a SIGIR-style resource or evaluation paper.

## Lessons learned from `SDATA-23-nature-journal`

- Scientific Data will reject a technically strong dataset paper if it is hard to follow for non-specialists.
- The paper must make the data easy to inspect:
  - explicit file structure
  - explicit schema
  - concrete examples
  - practical reuse guidance
- `Technical Validation` and `Usage Notes` are not optional in practice; they were central to turning the accepted STEREO version into a publishable Data Descriptor.
- Be careful with claims:
  - do not overclaim what the extraction or normalization means
  - state clearly what the data does not imply
  - avoid interpretations that could be mistaken for claims of misconduct
- Bias, limitations, and ethical-use concerns must be discussed explicitly.
- Editorial compliance still matters after scientific acceptance:
  - title/abstract format
  - Nature-style references
  - DOI formatting
  - corresponding-author details
  - separate production-quality figures
  - point-by-point response package for revision

## Current status in `SCIDATA_26_SR4ALL`

- The draft is no longer just a shell.
- Substantive sections already present:
  - `scidata--sr4all-pre.tex`
  - `scidata--sr4all-part1.tex` (`Background and Summary`)
  - `scidata--sr4all-part2.tex` (`Methods`)
- Supporting display items already present:
  - `table-filtering-stats.tex`
  - `table-field-cov.tex`
  - one embedded figure for the extraction pipeline example
- Supporting data artifacts already present:
  - `data/data_card.md`
  - `data/sr4all_full.jsonl`
- Strong current points:
  - title is already in good Scientific Data style
  - abstract is close to the right tone and scope
  - the corpus-construction pipeline is clearly structured
  - the Methods section already contains concrete counts, field coverage, and a detailed extraction/query-normalization description
- Major missing sections remain:
  - `Data Records` is empty
  - `Technical Validation` is empty
  - `Usage Notes` is empty
  - `Data Availability` is empty
  - `Code Availability` is empty
  - end matter is still missing: `Author Contributions`, `Competing Interests`, `Funding`, `Acknowledgments`
- Current technical/editorial issues visible in the files:
  - `scidata-sr4all-frame.tex` still uses an external `.bib` via `\bibliography{...}`
  - frame-file comments do not match the actual role of `part6` and `part7`
  - `Methods` currently contains footnotes for tool URLs
  - `Methods` uses a `\paragraph{Verify-then-repair pipeline.}` subheading that may need simplification for house style consistency
  - `SCIDATA_26_SR4ALL/README.md` appears empty, but `data/data_card.md` now provides a concrete local source for dataset structure and release wording
- Interpretation:
  - the paper already has a credible `Background and Summary` plus a fairly mature `Methods`
  - the submission is still blocked by missing descriptor-specific sections, not by lack of core narrative

## Phase 1: Setup

- Inventory what already exists in `SCIDATA_26_SR4ALL` and what is still missing.
- Use the accepted STEREO submission as the internal quality bar for section completeness and reviewer-readability.
- Preserve the current strengths in `Background and Summary` and `Methods`; focus effort on the missing Data Descriptor parts.

## Phase 2: Rewrite

- Keep the title descriptive, plain, and within Scientific Data limits.
- Rewrite the abstract to stay short, factual, and non-promotional.
- Keep the wording accessible to non-IR / non-LLM reviewers.
- Fold related work into `Background and Summary`.
- Rework comparative material into dataset-context material, not leaderboard-style comparison.
- Remove or heavily shrink retrieval-experiment content.
- Remove discussion/conclusion style sections; keep only factual limitations where needed.
- Avoid language that could make the paper read like a claim of scientific findings rather than a data resource.

## Add or complete the required sections

- `Data Records`
  - released files
  - file formats
  - schema / field definitions
  - repository link
- `Usage Notes`
  - example records
  - normalized-query example if retained
  - recommended filters or subsets
  - practical reuse guidance
  - ethics / misuse notes
- `Data Availability`
- `Code Availability`
- `Author Contributions`
- `Competing Interests`
- `Funding`
- `Acknowledgments`

## Phase 3: Technical Validation

- Treat this as the main bottleneck for submission readiness.
- Replace weak validation with a defensible validation design.
- Increase and justify sample size statistically.
- Use stratified sampling:
  - discipline
  - document length
  - extraction outcome category
- Validate extraction quality with stronger baselines where useful.
- Use scalable judging or review methodology where manual validation alone is too small.
- Add corpus-level descriptive statistics:
  - field coverage
  - extraction coverage
  - query normalization success
  - outlier inspection
- Add failure-mode discussion, not just headline validation scores.
- Make clear what validation supports and what remains uncertain.
- Document the validation procedure in enough detail to convince reviewers the resource is trustworthy.

## Phase 4: Internal review

- Circulate the full draft to co-authors with a hard deadline.
- Run a compliance pass against Scientific Data expectations:
  - no novelty or impact language
  - all required sections present
  - title and abstract within limits
  - figures and tables within journal expectations
  - data link ready
  - code link ready
- Check that reviewers without deep technical background can understand the paper end-to-end.
- If possible, get one read from someone outside the immediate project.

## Phase 5: Submission

- Submit as `Data Descriptor`.
- Prepare a single PDF with figures and tables embedded for round 1.
- A minimal cover letter is sufficient.
- Declare the arXiv preprint in the submission system.
- If needed, handle APC waiver or discount requests at submission time.

## Phase 6: Review timeline

- Initial QC: roughly 1-2 weeks.
- Editor assignment: roughly 1-4 weeks.
- Reviewer recruitment: roughly 4-10 weeks.
- Review: roughly 3-6 weeks.
- First decision: roughly month 3-5.
- Revision window: about 1 month, usually extendable on request.
- Round 2: roughly 2-3 more months.
- Possible acceptance/publication window: roughly month 6-9.

## Phase 7: Round 2 preparation

- Convert the manuscript into a machine-readable standalone `.tex` submission package.
- Avoid separate `.bib` / `.bbl` if following the local Scientific Data guideline strictly.
- Export figures as separate publication-quality files.
- Prepare a point-by-point response to reviewers.
- Be ready to submit highlighted changes and small reviewer-friendly examples if requested.
- Ensure the Zenodo deposit is final and matches the manuscript exactly.

## Immediate priorities for `SR4ALL`

- Finish `Data Records`.
- Finish `Technical Validation`.
- Finish `Usage Notes`.
- Add `Data Availability` and `Code Availability`.
- Add end matter sections.
- Remove or replace the current footnotes in `Methods`.
- Decide how to handle references for final Scientific Data packaging.
- Use `data/data_card.md` and the files in `data/` to write `Data Records` concretely, and add a manuscript-local packaging note only if it still adds value.
- Keep `Data Records` focused on released artifacts, layer linkage, and subset logic; leave detailed normalized-query examples to `Usage Notes`.
- Re-check references and submission packaging against Scientific Data requirements.

## Bottom line

- The main risk is not the framing anymore; it is incomplete dataset-description and validation work.
- The decisive step for submission readiness is a credible `Technical Validation` section plus complete Scientific Data end matter.
