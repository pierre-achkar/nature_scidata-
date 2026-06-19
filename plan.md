# Plan: Sci Data submission of Webis-SR4ALL-26

## Phase 1 — Setup and inventory 

- Read 3–5 recent Sci Data papers in adjacent areas (IR corpora, text mining datasets) to calibrate tone and structure.
- Inventory check: what already exists, what is missing, what needs expansion.

## Phase 2 — Rewrite 

**Cut and reframe:**
- New title — no "Large-Scale", no colons, ≤110 characters, descriptive only.
- Rewrite abstract — ≤170 words, no comparisons, no findings, no URLs.
- Fold Related Work into Background & Summary; remove gap-and-fill arc.
- Repurpose Table 1 as a list of integrated input sources, not a competitive comparison.
- Delete §4.2 retrieval experiment (or shrink to one paragraph as optional Data Overview).
- Delete Discussion and Conclusion. Salvage Limitations as a short factual subsection.

**Add:**
- New formal Data Records section: file list, schema, field definitions, repository link.
- Data Availability and Code Availability as proper sections (not footnotes).
- Author Contributions, Competing Interests, Funding statements.

## Phase 3 — Technical Validation expansion 

This is the highest-risk section and the bottleneck for submission readiness.

- Determine sample size statistically — 60 reviews is not defensible for a 32k corpus.
- Stratified sampling across (i) scientific discipline (use OpenAlex primary field), (ii) document length, and possibly (iii) extraction outcome category (mostly filled / partially filled / mostly null).
- Staged extraction validation: re-run a sample with stronger LLMs as a quality ceiling; use LLM-as-judge methodology to scale validation beyond manual review.
- Add descriptive statistics on the released corpus (field coverage by discipline, query normalization success rates, etc.).
- Sanity checks on outliers — flag and inspect extreme cases.
- Document the validation methodology fully — this section needs to convince reviewers that the corpus is trustworthy.

## Phase 4 — Internal review

- Full draft circulated to all co-authors with a hard deadline for comments.
- Compliance pass against Sci Data round-1 quality check criteria:
  - No novelty/impact language anywhere.
  - All required sections present.
  - Title and abstract within limits.
  - ≤8 figures, ≤10 tables.
  - Data accessible at the Zenodo link.
  - Code accessible at GitHub link.
- Final read by someone outside the immediate project, if possible.

## Phase 5 — Submission 

- Single PDF with figures and tables embedded.
- Blank cover letter is fine.
- Declare arXiv preprint on the submission form.
- If no DEAL coverage: request waiver/discount at the point of submission (cannot be requested later).
- Select article type: Data Descriptor.

## Phase 6 — Review process 

- Initial QC: 1–2 weeks.
- Editor assignment: 1–4 weeks.
- Reviewer recruitment: 4–10 weeks (the slow part).
- Reviewing: 3–6 weeks.
- First decision around month 3–5.
- Revision window: 1 month, extendable on request.
- Round 2: 2–3 months.
- Acceptance and immediate publication as Article in Press around month 6–9.

## Phase 7 — Round 2 requirements 

- Convert to machine-readable .tex (single standalone file, no separate .bib/.bbl).
- Export figures as separate files at publication resolution.
- Write point-by-point Response to Reviewers document.
- Confirm Zenodo deposit is final and matches the manuscript exactly.

