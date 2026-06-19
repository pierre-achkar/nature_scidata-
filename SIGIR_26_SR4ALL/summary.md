# Summary: Webis-SR4ALL-26 — A Large-Scale, Cross-Disciplinary Corpus of Systematic Reviews

**Submitted to:** SIGIR 2026 Resource Track (Paper #242) — **Rejected** (43% acceptance rate)

**Authors:** Pierre Achkar (Leipzig University; Fraunhofer ISI), Tim Gollub (Bauhaus-Universität Weimar), Arno Simons (TU Berlin), Harrisen Scells (University of Tübingen), Martin Potthast (Kassel University; hessian.AI; ScaDS.AI)

**Links:** [GitHub](https://github.com/webis-de/sigir26-sr4all) · [Zenodo](https://doi.org/10.5281/zenodo.18431942)

---

## 1. Problem Statement

Systematic reviews (SRs) are a central method for synthesizing scientific evidence. Conducting them is expensive, and automation of their **retrieval** and **screening** stages has received substantial research attention. However, existing evaluation resources are:

- Predominantly **biomedical** in domain focus
- **Limited in scale** (dozens to hundreds of topics)
- Missing broader disciplinary coverage needed to generalize IR and screening methods

---

## 2. Contribution

**Webis-SR4ALL-26** is a large-scale, cross-disciplinary corpus of **301,871 systematic reviews** spanning **27 scientific fields**, derived from OpenAlex. It includes:

- Resolved OpenAlex reference lists (full citation backbone)
- Structured methodological metadata extracted via LLM pipeline from full texts
- Normalized, executable Boolean query approximations of reported search strategies

---

## 3. Corpus Construction — Three-Stage Pipeline

### Stage 1: Data Collection and Filtering

| Step | Remaining | Δ |
|------|-----------|---|
| OpenAlex title search ("systematic review", "systematic literature review") | 485,446 | — |
| 1. Deduplication (DOI, OA-ID, normalized title) | 465,103 | −4.2% |
| 2. Title heuristic (explicit SR declaration, excl. updates) | 293,523 | −36.9% |
| 3. Non-English filtered out | 287,061 | −2.2% |
| 4. No valid DOI filtered out | 283,560 | −1.2% |
| 5. Update/revision titles excluded | 280,886 | −0.9% |
| + Benchmark integration (CLEF TAR 17–19, SysRev-Query, SysRev-Seed, CSMeD, AutoBool) | **301,871** | +7.5% |

From 65,906 reviews across benchmark datasets, 44,921 were already covered by OpenAlex; 20,985 were newly resolved and added.

**Domain distribution:** Medicine ~64%, Psychology 6%, Health Professions 5%, Biochemistry/Genetics/Mol. Bio. 4%, Social Sciences 3%, Neuroscience 3%; plus Engineering, CS, Economics, etc. in smaller shares.

### Stage 2: Full-Text Acquisition and Parsing

- PDF links from OpenAlex were used to attempt automated downloads
- **72,678 PDFs** successfully retrieved (24.1% of corpus)
- All PDFs parsed to Markdown using **PaddleOCR-VL** (0.9B vision-language model), chosen for its balance between accuracy and computational efficiency on complex scientific layouts

### Stage 3: Structured Information Extraction

An LLM-based pipeline extracts the following fields from full texts:
- Study objective
- Research questions
- Search strategies (Boolean queries or keyword lists)
- Inclusion and exclusion criteria
- Number of studies identified and included
- Temporal search restrictions
- Databases queried
- Citation chasing strategies

**Verify-Then-Repair Pipeline** (to avoid hallucinations):

1. **Primary Pass:** Qwen3-32B extracts all fields with verbatim evidence spans from the source document
2. **Two-stage verification:**
   - Approximate string matching against OCR text (tolerates minor noise)
   - MiniCheck (LLM-based factual verifier) checks semantic support
   - Extractions failing either check are set to `null`
3. **Repair Pass:** For `null` fields, a focused second extraction is run
4. **Final Validation:** Repair outputs undergo the same two-stage verification

---

## 4. Field Coverage Statistics

| Subset | Count | % |
|--------|-------|---|
| Total systematic reviews | 301,871 | 100% |
| w/ abstract | 227,208 | 75.3% |
| w/ full texts | 72,678 | 24.1% |
| w/ objective | 59,108 | 19.6% |
| w/ research questions | 14,934 | 4.9% |
| w/ keywords used | 36,028 | 11.9% |
| w/ Boolean queries | 28,251 | 9.4% |
| w/ inclusion criteria | 48,010 | 15.9% |
| w/ exclusion criteria | 24,914 | 8.3% |
| w/ date range | 61,951 | 20.5% |
| w/ databases queried | 9,283 | 3.1% |
| w/ paper counts retrieved | 46,590 | 15.4% |
| w/ paper counts included | 51,595 | 17.1% |
| w/ paper references (all reviews) | 301,871 | 100% |
| **Effectively usable subset** (objective + search strategy + criteria) | **38,292** | **12.7%** |
| w/ all fields present | 733 | 0.2% |

---

## 5. Qualitative Extraction Evaluation

60 reviews were manually examined (20 mostly-filled, 20 partially-filled, 20 mostly-null):

- **Mostly filled:** Pipeline reliably captured Boolean queries, study counts, eligibility criteria, date ranges, and objectives. Success correlated with clear document structure and explicit section headings.
- **Partially filled:** Verification stages frequently nullified correct extractions when information was spread across multiple sentences or required light abstraction (high precision, lower recall).
- **Mostly null:** Most failures were due to document type misalignment — records were errata, supplementary materials, or registration documents, not SR methodology documents.

---

## 6. Query Normalization

Reported search strategies are highly heterogeneous (Scopus syntax, PubMed MeSH tags, etc.) and cannot be directly executed across platforms. The paper normalizes them into unified Boolean expressions for OpenAlex:

- **Retained:** Topical terms, AND/OR/NOT operators
- **Removed:** Field tags (e.g., `TITLE-ABS-KEY`, `[mesh]`), language/publication-type filters
- **Temporal constraints:** Applied externally from extracted year-range metadata, not embedded in the Boolean string
- **Tool:** Qwen3-32B with few-shot prompting + lightweight rule-based post-processing for syntactic validity
- Queries that cannot be normalized (e.g., referencing external term lists) are set to `null`

---

## 7. Retrieval Demonstration

Normalized queries executed against OpenAlex `/works` endpoint. Only queries returning 1,000–250,000 results were used (smallest bucket to avoid runaway queries).

| Query Origin | # Reviews | Precision | Recall | F₁ | F₃ |
|---|---|---|---|---|---|
| Boolean queries | 12,005 | 0.014 | 0.245 | 0.019 | 0.050 |
| Keyword lists | 9,043 | 0.016 | 0.180 | 0.018 | 0.043 |

- Boolean strategies yield higher recall than keyword-only queries (0.245 vs. 0.180)
- Very low precision expected: queries are intentionally minimal and field-agnostic; reference lists include background literature, not only included studies
- Results represent retrieval behaviour under a simplified, cross-domain index — not a reproduction of original database searches

---

## 8. Comparison to Related Work

| Dataset | Domain | # Topics | Boolean Queries | Full Texts | Cross-Domain |
|---|---|---|---|---|---|
| Cohen et al. (2006) | Biomed | 15 | — | — | No |
| CLEF TAR 2017–2019 | Biomed | 50/30/49 | Yes | Partial | No |
| SysRev Query Collection | Biomed | 94 | Yes | — | No |
| SysRev Seed Collection | Biomed | 40 | Yes | Partial | No |
| CSMeD | Biomed+CS | 325 | Yes | Partial | Minimal |
| AutoBool | Biomed | 65,588 | — | Partial | No |
| Hannousse et al. | CS only | 7 | — | — | No |
| **Webis-SR4ALL-26** | **27 fields** | **301,871** | **Partial** | **Partial** | **Yes** |

---

## 9. Intended Use Cases

1. **Benchmarking retrieval and screening** methods against review reference lists
2. **Cross-domain comparison** of retrieval and screening performance
3. **Training and evaluating extraction models** for review artifacts (objectives, queries, criteria)
4. **Meta-science research:** comparative analyses of SR practices across disciplines and time
5. **Science communication and policy studies** (how SRs diffuse into public discourse)

---

## 10. Limitations (Acknowledged by Authors)

- **Title-based SR identification** favors precision but misses SRs that don't self-declare in the title
- **Full-text availability** only 24.1% — limits extraction coverage
- **Strict verification** prioritizes precision over recall; implicitly stated or distributed information is often lost
- **Reference lists ≠ included-study gold standards** — reviews cite background literature too
- **Normalized queries** are simplified approximations; they may not capture database-specific syntax or manual tuning from the original formulations

---

## 11. Peer Review Outcome

The paper was **rejected** (3 reviews, all "Lean to Reject"):

**Common criticisms:**
- The "large-scale" claim is undermined by the effectively usable subset being only 38,292 reviews (12.7%)
- Despite 27 fields, the corpus remains ~64% biomedical, weakening the cross-disciplinary claim
- Extremely low retrieval precision (~0.015) with no comparison to existing retrieval models
- No ablation experiments on the extraction pipeline; precision/recall of extraction not quantitatively reported
- Lack of a concrete, grounded application scenario with test data
- Ground-truth issue (reference lists vs. included-study sets) should be addressed more prominently, not buried in limitations
- The small qualitative evaluation (60 reviews) is insufficient for a corpus of this scale
- Suggestion to compare LLM extractions against smaller curated collections for calibration

**Positive aspects noted:**
- Novelty: clearly larger and more cross-disciplinary than any prior resource
- Availability: dataset and code are public at review time
- Pipeline is clearly described and reproducible

---

## 12. Conclusion

Webis-SR4ALL-26 is the first large-scale, cross-disciplinary systematic review corpus, integrating 301,871 reviews with OpenAlex citation backbones, LLM-extracted methodological metadata, and normalized executable Boolean queries — all under an open infrastructure. It is designed to support IR benchmarking, screening research, extraction method development, and meta-science studies. The paper was rejected at SIGIR 2026 primarily due to concerns about the usable subset size, the biomedical bias in the cross-disciplinary claim, and the lack of a concrete validated use case, but the reviewers acknowledged strong novelty and resubmission potential (e.g., ICTIR or SIGIR-AP via Revise & Resubmit).
