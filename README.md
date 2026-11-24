# AirAware AI

**AI-Based Air Quality Information and Guidance System**

AI Engineering semester project | Phase 1: Topics 1–4

## 1. Project Overview

AirAware AI is a proposed web-based assistant that helps Malaysian residents understand Air Pollutant Index (API) readings, air pollutants, environmental standards and general environmental precautions using official Department of Environment (DOE) documents.

### Problem Statement

Official air quality information can be technical and distributed across multiple documents. Users may find it difficult to interpret API readings and locate relevant explanations. AirAware AI aims to provide understandable, source-grounded answers through a unified natural-language interface.

### Objectives

1. Design a document-grounded AI air quality information system using official Malaysian environmental documents.
2. Develop a web-based assistant using semantic retrieval and Retrieval-Augmented Generation (RAG).
3. Evaluate retrieval relevance, answer correctness, citation reliability, safety and response time.

### Target Users and Scope

Target users include Malaysian residents, students, outdoor workers and members of the public.

**In scope:** English questions, classification of user-supplied API values using verified rules, document-grounded explanations, citations and safe handling of unsupported questions.

**Out of scope:** live air quality monitoring, forecasting, medical diagnosis and personalised medical advice.

## 2. Official Data Sources

| Source | Format | Purpose | Current prepared corpus |
|---|---|---|---|
| [New Malaysia Ambient Air Quality Standard](https://www.doe.gov.my/wp-content/uploads/2021/10/Air-Quality-Standard-BI.pdf) | PDF | Pollutants and environmental standards | 3 chunks |
| [DOE Air Pollutant Index information](https://www.doe.gov.my/2021/10/04/english-air-pollutant-index-api/) | Web page converted to TXT | API interpretation and categories | Selected but not represented |

Both sources are publicly accessible institutional documents. Reuse and redistribution permissions remain to be verified. Public access does not establish public-domain status.

## 3. Project Architecture

Planned query flow:

```text
User input -> Scope and safety control -> Query processing
    -> Information retrieval -> RAG answer generation
    -> Citation and evidence check -> User response
```

Unsupported questions receive a safe response. API classification uses deterministic rules rather than relying on generated numerical ranges. Semantic retrieval and RAG implementation are planned for Topic 7, not claimed as completed.

## 4. Lab Progress

| Topic | Focus | Work and evidence |
|---|---|---|
| Lab 1 | AI system analysis and project scoping | Project problem, objectives, target users, scope, system map and Responsible AI risks |
| Lab 2 | Requirements and architecture | Functional, non-functional and Responsible AI requirements; evaluation criteria; architecture decisions and traceability |
| Lab 3 | Data preparation and pipeline | Pathway A (PDF/TXT), source inventory, extraction, cleaning, chunking, lineage and pipeline documentation |
| Lab 4 | Data quality and responsible data practices | Hand-off verification, quality inventory, manual inspection, validation, triage, exact deduplication, coverage, bias and governance review |

### Topic 2 — Key Evaluation Targets

| Requirement | Planned target |
|---|---|
| NFR1 | p90 response time <= 5 seconds |
| NFR2 | Answer correctness >= 85% |
| NFR3 | Recall@5 >= 85% |
| RAI1 | Citation-source match >= 95% |
| RAI2 | Correct handling of out-of-scope questions >= 95% |

These are evaluation targets, not achieved system results. Refer to the Topic 2 requirements and evaluation documents for the complete specification.

### Topic 3 — Data Preparation

Selected pathway: A (PDF/TXT). The preparation workflow is source selection, ingestion, inspection, extraction and cleaning, paragraph-aware chunking, output validation and lineage recording. The original prepared text and pipeline outputs are retained for reproducibility. The current exported corpus contains only the PDF source; the TXT source still requires integration.

### Topic 4 — Data Quality Findings

| Finding | Result |
|---|---|
| Chunks before exact deduplication | 3 |
| Chunks after exact deduplication | 3 |
| Exact duplicates | 0 |
| Missing text / source filename | 0 / 0 |
| Possible corrupted characters / noisy whitespace | 0 / 0 |
| Unexpected source filenames | 0 |
| Missing page metadata | 3 |
| Source coverage | PDF: 100%; TXT: 0% |

Pandera execution results must be checked against the notebook and validation CSV. Exact deduplication does not establish semantic uniqueness. PDF table accuracy, source currency and reuse rights remain unverified.

**Quality gate: HOLD for full downstream use.** Resolve critical coverage, provenance, accuracy and rights issues before using the corpus for full RAG development. See [Week 4 Data Quality Report](docs/week4_data_quality_report.md).

## 5. Repository Structure

Expected layout for the Lab 1–4 deliverables (verify against the actual repository):

```text
AirAware-AI/
├── README.md
├── docs/
│   ├── week1_project_scope.md
│   ├── week1_system_map.png
│   ├── week2_requirements.md
│   ├── week2_evaluation_criteria.md
│   ├── week2_architecture_decisions.md
│   ├── week2_architecture_v1.png
│   ├── week3_data_inventory.md
│   ├── week3_pipeline_diagram.png
│   ├── week3_pipeline_decisions.md
│   ├── week4_data_quality_report.md
│   ├── week4_validation_failures.csv
│   ├── week4_duplicate_review.csv
│   └── week4_coverage_by_source.png
├── notebooks/
│   ├── week3_pipeline.ipynb
│   └── week4_quality.ipynb
└── data/
    ├── raw/
    ├── processed/
    │   └── prepared_text.jsonl
    ├── week3_manifest.json
    ├── pipeline_v1/
    │   └── documents/
    │       └── pipeline_manifest.json
    ├── prepared_chunks.jsonl
    ├── chunks.pkl
    ├── prepared_chunks_clean.jsonl
    └── chunks_clean.pkl
```

The Topic 3 pipeline folder also contains its generated prepared outputs. Raw and prepared files should only be committed if authorised; otherwise document their approved storage location and provide non-sensitive execution evidence.

## 6. Topic 7 (Week 9) — Reviewed Corpus Hand-off

Topic 7 must use the **reviewed Topic 4 corpus**, not the original Topic 3 corpus.

| File | Role |
|---|---|
| `data/prepared_chunks_clean.jsonl` | Preferred inspectable and auditable reviewed corpus |
| `data/chunks_clean.pkl` | Compatibility corpus for later notebook code |
| `data/prepared_chunks.jsonl` and `data/chunks.pkl` | Original hand-off inputs; retain for traceability only |
| `data/processed/prepared_text.jsonl` | Original Topic 3 preparation output; retain for lineage |

Before Topic 7, resolve the HOLD conditions, regenerate the reviewed outputs after corrections, rerun relevant Topic 4 checks, verify that JSONL and PKL record counts match, and update the quality report. Do not silently fall back to the original Topic 3 files. Only load trusted project-generated pickle files.

Topic 7 will introduce embeddings, vector indexing, semantic retrieval and RAG. Topic 8 (Week 10) will evaluate retrieval, generation, safety and grounding against the Topic 2 targets.

## 7. Responsible AI and Next Actions

- Include the missing DOE API TXT source and verify official classification ranges.
- Recover page-level provenance and verify extracted table values, units and averaging periods.
- Verify source versions and reuse permissions before downstream use or redistribution.
- Preserve citations and refuse unsupported or out-of-scope questions.
- Avoid collecting unnecessary personal information and establish source update and retention responsibilities.
- Evaluate system-level correctness, coverage and grounding in Topic 8; data-level findings alone do not establish final fairness.

## 8. Tools and Reproducibility

Google Colab, Python, pypdf, pandas, Pandera, Matplotlib, Draw.io and GitHub are used for the Phase 1 work. Run the Topic 3 preparation notebook and Topic 4 quality notebook in order when rebuilding the corpus. Keep manifests and quality evidence alongside the reviewed outputs. No foundation-model API key is required for Topic 4.

## Project Status

Phase 1 documentation and data-quality assessment through Lab 4. Downstream implementation and system evaluation are pending. The reviewed corpus is not yet approved for full downstream use.

