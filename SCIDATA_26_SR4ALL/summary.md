# Summary: A Cross-Disciplinary Corpus of Systematic Reviews

**Submitted to:** Nature Scientific Data (data descriptor format)

**Authors:** Pierre Achkar (Leipzig University; Fraunhofer ISI), Tim Gollub (Bauhaus-Universität Weimar), Arno Simons (TU Berlin), Harrisen Scells (University of Tübingen), Martin Potthast (Kassel University; hessian.AI; ScaDS.AI)

**Corresponding author:** Pierre Achkar (pierre.achkar@uni-leipzig.de)

---

## Context

This is the **Nature Scientific Data resubmission** of the same Webis-SR4ALL-26 corpus previously submitted and rejected at SIGIR 2026 (Resource Track). The dataset and pipeline are unchanged; the paper is reformatted as a Scientific Data **data descriptor** with section structure mandated by the journal: Background & Summary, Methods, Data Records, Technical Validation, Usage Notes, Data Availability, Code Availability.

Title follows SciData rules: ≤110 characters, no colons or parentheses, no acronyms, no advertising words (novel, first, large-scale, AI-ready), capitalize only first word and proper nouns.

**Current status:** Background & Summary and Methods sections are drafted. Data Records, Technical Validation, Usage Notes, Data Availability, and Code Availability are placeholder stubs (just section headers).

---

## 1. Problem Statement

Systematic reviews (SRs) are the standard method for synthesizing evidence across scientific fields. Automating their **retrieval** and **screening** stages is an active research area, but existing evaluation resources are:

- Predominantly **biomedical** in domain focus
- **Limited in scale** (dozens to hundreds of topics)
- Missing the cross-disciplinary coverage needed to generalize IR and screening methods

---

## 2. Contribution

**Webis-SR4ALL-26** is a corpus of **301,871 systematic reviews** spanning **27 scientific fields**, derived from OpenAlex. It provides:

- Resolved OpenAlex reference lists (full citation backbone for all reviews)
- Structured methodological metadata extracted via LLM pipeline from full texts
- Normalized, executable Boolean query approximations of reported search strategies

---

## 3. Corpus Construction — Three-Stage Pipeline

### Stage 1: Data Collection and Filtering

| Step | Remaining |
|------|-----------|
| OpenAlex title search ("systematic review", "systematic literature review") | 485,446 |
| Deduplication (DOI, OA-ID, normalized title) | 465,103 |
| Title heuristic (explicit SR declaration) + language + DOI filters | 280,886 |
| + Benchmark integration (CLEF TAR 17–19, SysRev-Query, SysRev-Seed, CSMeD, AutoBool) | **301,871** |

From 65,906 benchmark reviews, 44,921 were already covered by OpenAlex; 20,985 were newly resolved and added.

**Domain distribution:** Medicine ~64%, Psychology 6%, Health Professions 5%, Biochemistry/Genetics/Mol. Bio. 4%, Social Sciences 3%, Neuroscience 3%; plus Engineering, CS, Economics, and others.

### Stage 2: Full-Text Acquisition and Parsing

- PDF links from OpenAlex used for automated download
- **72,678 PDFs** successfully retrieved (24.1% of corpus)
- All PDFs parsed to Markdown using **PaddleOCR-VL** (0.9B vision-language model) for its accuracy/efficiency balance on complex scientific layouts

### Stage 3: Structured Information Extraction

An LLM-based **verify-then-repair** pipeline extracts the following fields from full texts:

- Study objective
- Research questions
- Search strategies (Boolean queries or keyword lists)
- Inclusion and exclusion criteria
- Number of studies identified and included
- Temporal search restrictions
- Databases queried
- Citation chasing strategies

**Verify-Then-Repair Pipeline:**

1. **Primary Pass:** Qwen3-32B extracts all fields with verbatim evidence spans from the source
2. **Two-stage verification:**
   - Approximate string matching against OCR text (tolerates minor parsing noise)
   - MiniCheck (LLM-based factual verifier) checks semantic support
   - Extractions failing either check are set to `null`
3. **Repair Pass:** A focused second extraction is run for any `null` fields
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

## 5. Query Normalization

Reported search strategies are heterogeneous (Scopus syntax, PubMed MeSH tags, etc.) and normalized into unified Boolean expressions executable via the OpenAlex API:

- **Retained:** Topical terms, AND/OR/NOT logical operators
- **Removed:** Field tags (e.g., `TITLE-ABS-KEY`, `[mesh]`), language/publication-type filters
- **Temporal constraints:** Applied externally from extracted year-range metadata
- **Tool:** Qwen3-32B with few-shot prompting + lightweight rule-based post-processing
- Two variants produced: full Boolean queries (from reported search strings) and keyword-based queries (where no full Boolean is available)

---

## 6. Intended Use Cases

1. **Benchmarking retrieval and screening** methods against review reference lists across 27 fields
2. **Cross-domain comparison** of retrieval and screening performance
3. **Training and evaluating extraction models** for review artifacts (objectives, queries, criteria)
4. **Meta-science research:** comparative analyses of SR practices across disciplines and time
5. **Science communication and policy studies**

---

## 7. Comparison to Related Work

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

## 8. Sections Still to Write

The following sections are currently empty stubs:

- **Data Records:** Should describe the dataset files, their formats, and how to access them
- **Technical Validation:** Should document validation of the extraction pipeline (qualitative evaluation of 60 reviews, retrieval demonstration results)
- **Usage Notes:** Should provide guidance on how to load and use the dataset layers
- **Data Availability:** Dataset links (Zenodo, etc.)
- **Code Availability:** Pipeline code links (GitHub)

---

## 9. Key Differences from SIGIR Submission

| Aspect | SIGIR 2026 | Nature Scientific Data |
|--------|-----------|----------------------|
| Paper type | Resource paper | Data descriptor |
| Title | Webis-SR4ALL-26: A Large-Scale, Multi-Domain Corpus... | A cross-disciplinary corpus of systematic reviews |
| Abstract limit | Unspecified | ≤170 words, no novelty claims |
| Evaluation emphasis | Retrieval demonstration results | Technical validation of data quality |
| Sections | Standard IR paper | Background & Summary / Methods / Data Records / Technical Validation / Usage Notes / Data/Code Availability |
| Status | Rejected | In preparation |
