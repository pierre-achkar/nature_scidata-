# Project orientation

This repository supports the resubmission of `Webis-SR4ALL-26` to *Nature Scientific Data* and keeps both the prior SIGIR submission and an accepted Scientific Data paper from the same research group for reference.

## Main goal

- Primary target: prepare `SCIDATA_26_SR4ALL` as a publishable *Scientific Data* `Data Descriptor`.
- Secondary reference goal: use the accepted `SDATA-23-nature-journal` submission as an internal model for structure, review handling, and editorial expectations.

## Root-level files and directories

### `SCIDATA_26_SR4ALL/`

- Main working directory for the *Scientific Data* resubmission of `SR4ALL`.
- This is the most important folder for current work.
- Contains the LaTeX manuscript split into section files, plus local tables and figures.

### `data/`

- Local dataset workspace for the released `SR4ALL` artifacts.
- Use this directory when drafting or checking:
  - `Data Records`
  - `Usage Notes`
  - `Data Availability`
  - dataset-facing parts of `Technical Validation`
- Inspect the actual files in this directory before changing file counts, names, schemas, or release wording.
- `data/data_card.md` is the first file to read here.

### `SIGIR_26_SR4ALL/`

- Earlier SIGIR 2026 submission of the same dataset.
- Use this as source material for content, prior framing, tables, and comparisons.
- Do not use it as the stylistic target for the resubmission.

### `SDATA-23-nature-journal/`

- Accepted *Scientific Data* submission from the same research group.
- Use this as the main reference for:
  - section structure
  - tone and caution level
  - `Data Records`, `Technical Validation`, and `Usage Notes`
  - reviewer expectations
  - revision packaging

### `scientific_data_submission_guidelines.md`

- Local copy of the relevant *Scientific Data* submission guidance.
- Read this before making submission-format decisions.
- Use it to check title, abstract, sectioning, data/code statements, references, and revision packaging.

### `SR4ALL_scientific_data_notes.md`

- Live planning and status document for the current resubmission.
- Contains:
  - the current phase-based plan
  - lessons learned from the accepted `SDATA-23-nature-journal`
  - current known gaps in `SCIDATA_26_SR4ALL`

### `plan.md`

- Earlier plan document for the Scientific Data submission.
- Mostly superseded by `SR4ALL_scientific_data_notes.md`.
- Keep as archive/reference unless explicitly needed.

### `to_dos/`

- Planning workspace for paper-development tasks.
- Contains the active `progress_board.md` and one markdown file per issue.
- This is the main operational planning area.

### `writing_tipps.txt`

- Local prose and LaTeX writing preferences.
- Especially important for:
  - sentence clarity
  - citation phrasing
  - table/figure conventions
  - LaTeX hygiene

### `AGENTS.md`

- Root-level startup instructions for future work in this repository.
- Read this file first each time.

## Contents of `SCIDATA_26_SR4ALL/`

### `scidata-sr4all-frame.tex`

- Root LaTeX document for the Scientific Data manuscript.
- This is the file that ties all section files together.

### `scidata--sr4all-pre.tex`

- Front matter:
  - title
  - authors
  - affiliations
  - corresponding author
  - abstract

### `scidata--sr4all-part1.tex`

- `Background and Summary`

### `scidata--sr4all-part2.tex`

- `Methods`

### `scidata--sr4all-part3.tex`

- `Data Records`
- Currently a key missing section.

### `scidata--sr4all-part4.tex`

- `Technical Validation`
- Currently a key missing section and the main scientific bottleneck.

### `scidata--sr4all-part5.tex`

- `Usage Notes`
- Currently missing and important for reviewer-facing usability.

### `scidata--sr4all-part6.tex`

- `Data Availability`

### `scidata--sr4all-part7.tex`

- `Code Availability`
- Note: despite frame-file comments, this file is not currently the end-matter section.

### `scidata--sr4all-lit.bib`

- Bibliography source for the current draft.
- Check against Scientific Data packaging expectations before final submission.

### `tables/`

- Local table files for the Scientific Data manuscript.
- Currently includes:
  - metadata filtering statistics
  - field coverage statistics

### `figures/`

- Local figure assets for the Scientific Data manuscript.
- Currently includes at least the extraction example figure.

### `summary.md`

- Snapshot summary of the current `SCIDATA_26_SR4ALL` status.
- Useful for quick orientation, but not the main live planning document anymore.

### `README.md`

- Currently empty.
- If needed, this is a good place for packaging or build notes specific to `SCIDATA_26_SR4ALL`.

## Contents of `data/`

### `data_card.md`

- Local description of the released `SR4ALL` data package.
- Primary starting point for:
  - released file inventory
  - field descriptions
  - stated corpus counts
  - reuse scenarios and limitations

### `sr4all_full.jsonl`

- Main JSONL release artifact currently present in the repository.
- Inspect representative records directly when manuscript text needs concrete examples or field verification.

## Contents of `SIGIR_26_SR4ALL/`

- Prior SIGIR paper source.
- Useful for:
  - earlier phrasing
  - prior tables
  - retrieval demonstration material
  - original bibliography
  - reviewer feedback context via `reviews.txt`

Key files:

- `sigir26-sr4all-frame.tex`: root LaTeX file
- `sigir26-sr4all-pre.tex`: front matter
- `sigir26-sr4all-part1.tex` to `part5.tex`: paper body sections
- `sigir26-sr4all-sum.tex`: summary or condensed material
- `table-*.tex`: paper tables
- `summary.md`: project summary for the SIGIR version
- `reviews.txt`: SIGIR reviewer feedback

## Contents of `SDATA-23-nature-journal/`

- Accepted reference project for a different dataset paper.
- Important subdirectories:

### `sdata23-scientific-text-reuse-corpus-paper-revision1/`

- Revised manuscript version used during the Scientific Data review process.
- Best reference for:
  - reviewer-driven improvements
  - section content
  - Data Descriptor structure

### `sdata23-scientific-text-reuse-corpus-paper-final/`

- Final accepted manuscript version.
- Best reference for end-state formatting and presentation.

### `sdata23-organization/`

- Review and process materials:
  - review letters
  - rebuttal drafts
  - copyright/proof files

### `sdata23-scientific-text-reuse-corpus-figures/`

- Figure assets for the accepted paper.

### `sdata23-scientific-text-reuse-corpus-material/`

- Supporting reference material archive.

### `sdata22-scientific-text-reuse-corpus-paper-submitted/`

- Earlier submitted version before the later accepted revision.
- Useful when comparing what changed across the process.

## Practical startup workflow

When beginning a new task in this repository:

1. Read `AGENTS.md`.
2. Read this file.
3. Read `SR4ALL_scientific_data_notes.md`.
4. Read `scientific_data_submission_guidelines.md`.
5. Check `to_dos/progress_board.md`.
6. Identify the active target:
   - usually `SCIDATA_26_SR4ALL`
   - sometimes `SDATA-23-nature-journal` for reference
   - sometimes `SIGIR_26_SR4ALL` for source reuse
7. If the task concerns dataset description, validation, or availability, inspect `data/data_card.md` and the relevant files in `data/`.
8. Read `writing_tipps.txt` before substantial prose edits.

## Current working assumptions

- The active manuscript target is `SCIDATA_26_SR4ALL`.
- The main missing work is in:
  - `Data Records`
  - `Technical Validation`
  - `Usage Notes`
  - availability statements
  - end matter
- The strongest local reference for how to satisfy Scientific Data reviewers is `SDATA-23-nature-journal`.

## Guidance for future edits

- Prefer Scientific Data tone: descriptive, careful, inspectable, and non-promotional.
- Avoid carrying over SIGIR-style framing, especially strong comparative or performance-first rhetoric.
- Keep reviewer-readability in mind: non-specialists must be able to understand the manuscript structure and the released resource.
- When uncertain about packaging, check `scientific_data_submission_guidelines.md` before making assumptions.
