# Week 3 Pipeline Decisions — AirAware AI

## Requirements and sources

| Requirement | Selected source / traceability |
|---|---|
| FR2 | DOE API information TXT; verify official classification ranges before use. |
| FR3 | DOE ambient air quality standard PDF and API TXT for grounded explanations. |
| FR4 / RAI1 | Preserve source identity and source-to-output mappings for citations. |
| NFR3 | Prepare text chunks for later semantic retrieval; retrieval performance is not yet measured. |

- [DOE ambient air quality standard PDF](https://www.doe.gov.my/wp-content/uploads/2021/10/Air-Quality-Standard-BI.pdf)
- [DOE API information webpage](https://www.doe.gov.my/2021/10/04/english-air-pollutant-index-api/) — saved as `doe_api_information.txt`.

## Part B comparison and selected configuration

| Approach A | Approach B | Observed evidence | Selection and trade-off |
|---|---|---|---|
| Fixed-size chunks (500 characters) | Paragraph-aware chunks (500 characters) | PDF: 1 page, 1,464 extracted characters, 1,457 cleaned characters; both methods produced 3 chunks and identical displayed 180-character previews. | Select paragraph-aware chunking to preserve paragraph boundaries where possible. No improvement is demonstrated by these results; long paragraphs still split at fixed boundaries. |

TXT comparison and Part C execution results: pending verification.

## Pipeline decisions

- Pathway A (PDF/TXT): extract PDF text with pypdf or read UTF-8 TXT; normalize spaces/tabs; split into paragraph-aware chunks of at most 500 characters; export JSONL.
- ETL: extract and transform documents before loading prepared records into storage for future retrieval.
- Batch processing: static documents are processed on demand; no live feed or streaming is needed.
- Accepted limitations: PDF tables may lose structure; figures are not automatically interpreted; page-level mapping is not supplied by the original Cell 8A; source currency and API ranges require verification.
- Part B outputs: `data/processed/prepared_text.jsonl` and `data/week3_manifest.json`.
- Part C expected outputs: `data/pipeline_v1/documents/prepared_text.jsonl` and `data/pipeline_v1/documents/pipeline_manifest.json`. Verify actual paths and both source mappings after execution.
- Provenance/access: retain exact source filenames, original URLs, fingerprints and source-to-output mappings. Public access does not establish redistribution permission; verify reuse conditions before committing data.

## Stage contracts and traceability

| Stage | Contract / evidence | Failure response |
|---|---|---|
| Ingest | Exact selected PDF/TXT exists under data/raw and use is permitted. | Stop for missing input; verify path and access. |
| Inspect | Source is readable; extracted text is nonempty; inspect representative content. | Stop or flag invalid structure or unreadable text. |
| Prepare | Selected cleaning and 500-character paragraph-aware chunking produce JSONL records. | Stop or report transformation failure. |
| Validate | Output exists, is nonempty and has a recorded fingerprint; inspect a representative record. | Stop for missing or empty output. |
| Record lineage | Source(s) link to exact output(s) in the manifest with fingerprints. | Stop/report missing mapping or metadata. |

## Execution verification

Cell 8A as supplied processes one source (`inputs[0]`) and writes a single output in write mode. Adapt it to preserve both sources or use distinct output locations and mappings; do not overwrite the PDF output with TXT. Verify Cell 9 repeatability results, both source mappings and actual output counts before marking C1/C2 complete. This document records the selected design and observed Part B PDF evidence, not a verified successful Part C run.
