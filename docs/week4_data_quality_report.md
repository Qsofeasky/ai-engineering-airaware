# Data Quality, Bias, and Responsible Data Report — AirAware AI

## 1. Data Quality Scorecard

| Dimension | Rating (1–5 / N.V.) | Evidence | Action / limitation |
|---|---:|---|---|
| Completeness | 2 | Only one of two selected sources is represented; all three chunks lack page metadata. | Include DOE API TXT and recover page references. |
| Consistency | N.V. | All three chunks have source names; no noisy whitespace or replacement characters detected. | Verify terminology, units and table structure against the original PDF. |
| Accuracy | N.V. | Automated text checks do not establish factual accuracy. | Compare extracted values and text with official sources. |
| Timeliness | N.V. | Currency of the standards has not been verified. | Check official document versions and dates. |
| Uniqueness | N.V. | Three chunks before and after exact deduplication; zero exact duplicates. | Review near-duplicates and conflicting versions before assigning an overall rating. |

The completeness rating is a provisional engineering judgement on a 1–5 scale (1 = poor, 5 = excellent), reflecting the confirmed missing source and metadata. Other dimensions are not fully verified.

## 2. Validation and Data-Defect Findings

The A2 inventory contains three chunks from `Air-Quality-Standard-BI.pdf`. Chunk lengths are 500, 499 and 452 characters (mean 483.67).

| Rule / quality concern | Observable condition | Failures | Percentage | Example / decision |
|---|---|---:|---:|---|
| Text present | Non-empty trimmed text | 0 | 0% | No empty chunks; hard fail if detected. |
| Source metadata | Non-empty source | 0 | 0% | All chunks have PDF filename; hard fail if missing. |
| Minimum useful length | char_count >= 100 | 0 | 0% | Minimum 452; warning and review if below threshold. |
| Corrupted characters | corrupted_char == False | 0 | 0% | No detected null or replacement characters; review if flagged. |
| Expected source | expected_doe_source == True | 0 | 0% | All filenames match the expected list; review unexpected sources. |
| Noisy whitespace | noisy_whitespace == False | 0 | 0% | No flagged chunks; review if detected. |
| Page provenance | Page metadata present (manual check) | 3 | 100% | Chunks 0–2 have page=None; recover references. |
| Source coverage | Both selected sources represented (manual check) | 1 of 2 sources missing | 50% | DOE API TXT absent; process and integrate. |

The counts above are supported by the A2 inventory and confirmed source counts, not an independently inspected Cell 4 Pandera execution. Verify against `week4_validation_failures.csv` before submission. Noisy whitespace, page provenance and source coverage are inventory/manual checks rather than the supplied Pandera rules. Inconsistent numerical relationships, stale information and broken word boundaries remain uncertain pending manual comparison.

## 3. Duplicate and Anomaly Findings

- Before exact deduplication: 3 chunks.
- After exact deduplication: 3 chunks.
- Exact duplicates: 0 (0%).
- No chunks were removed by exact deduplication. Existing source filenames were retained, but page references remain missing.
- Chunk lengths range from 452 to 500 characters; no length warning under the selected 100-character threshold.
- Possible broken word boundaries and loss of PDF table structure require manual verification. Contradictions, near-duplicates and superseded versions have not been verified.

## 4. Representation, Coverage, and Bias Assessment

| Required area | Expected evidence | Actual evidence | Gap / uncertainty |
|---|---|---|---|
| API definition | Official DOE API explanation | Selected TXT source absent | Source coverage gap |
| API categories and ranges | Official classification ranges | Not verified in PDF chunks | Potential topic coverage gap |
| Air pollutants | Official pollutant information | DOE standards PDF represented | Detailed coverage N.V. |
| Ambient air quality standards | Correct values, units and averaging periods | DOE standards PDF represented | Extraction accuracy N.V. |
| Source references | Traceable source metadata | PDF filename present; page missing | Provenance gap |

Source distribution: PDF 3 chunks (100%); TXT 0 chunks (0%). Unequal chunk counts do not establish unfairness or complete topic coverage.

| Bias type | Evidence | Likely origin | Potential downstream impact | Mitigation | Topic 8 test |
|---|---|---|---|---|---|
| Representation bias risk | Selected TXT source absent from prepared corpus | Pipeline (suspected) | Incomplete or unsupported API answers | Include TXT and validate topic coverage | Retrieval coverage, API classification correctness and grounding |
| Measurement-related bias risk | PDF standards are represented as extracted text chunks; preservation of table relationships is N.V. | Proxy | Incorrect interpretation of values, units or averaging periods | Preserve table structure and compare with original PDF | Numerical accuracy, unit correctness and citation match |
| Historical bias risk | Currency of official standards is N.V. | Source | Potential outdated explanations | Verify current official versions | Compare answers with current standards |

Propagation paths:

- Representation: selected TXT absent from prepared output → PDF-only corpus → reduced retrieval opportunities for API topics → potentially incomplete or unsupported answers.
- Measurement: PDF extraction and chunking → possible loss of table relationships → retrieval of values without correct context → potentially incorrect environmental explanations.
- Historical: unverified document currency → potentially outdated corpus → retrieval of superseded standards → potentially outdated answers.

Only the missing-source condition is confirmed. The exact cause and the other bias risks require verification. Final system fairness and performance must be evaluated in Topic 8 (Week 10).

## 5. Privacy, Consent, Rights/Access, and Data Governance

| Governance area | Evidence | Status | Required action / owner |
|---|---|---|---|
| Source ownership, version and provenance | DOE Malaysia; source URLs known; page references missing and currency unverified | Gap | Project developer: verify versions and metadata |
| Rights/access | Public institutional sources; reuse permissions unverified | To verify | Project developer: verify terms before redistribution |
| Personal/sensitive data | Environmental documents; no unnecessary personal data identified, full inspection N.V. | Unknown pending full review | Project developer: inspect corpus and future sources |
| Consent | Current scope uses institutional environmental documents, not personal records | N/A | Review if personal data is introduced |
| Update, retention and removal | Formal procedure not established | Gap | Project developer: define version control, periodic checks and removal of superseded data |

Selected source references:

- DOE New Malaysia Ambient Air Quality Standard: https://www.doe.gov.my/wp-content/uploads/2021/10/Air-Quality-Standard-BI.pdf
- DOE Air Pollutant Index information: https://www.doe.gov.my/2021/10/04/english-air-pollutant-index-api/

Public accessibility does not establish public-domain status or permission to redistribute. Restrict redistribution until reuse rights are verified. The TXT source is selected but not included in the current prepared corpus.

## 6. Mitigation Plan and Residual Risk

| Issue | Evidence | Action | Owner / timing | Residual risk |
|---|---|---|---|---|
| Missing TXT source | 0 TXT chunks | Process and merge TXT; rerun quality checks | Project developer / before downstream RAG use | Topic coverage may still be incomplete |
| Missing page metadata | 3 of 3 chunks | Recover verified page references | Project developer / before indexing | Document-level citations may remain less precise |
| Potential table extraction errors and broken boundaries | Extracted text chunks; exact defects N.V. | Compare with original PDF; preserve tables and improve chunk boundaries where necessary | Project developer / before indexing | Some context may still be lost |
| Unverified currency | Version/current status N.V. | Check current DOE sources and establish update procedure | Project developer / before downstream use | Standards may change later |
| Unverified reuse rights | Public access only established | Verify permission; restrict sharing until resolved | Project developer / before redistribution | Some uses may remain restricted |
| Unverified semantic uniqueness | Exact duplicate count only | Review near-duplicates and contradictions | Project developer / before indexing | Similar or conflicting content may remain |

## 7. Impact on Topic 2 Requirements / Evaluation Criteria

| Requirement | Potential impact |
|---|---|
| FR2 — API classification | Missing authoritative API source limits verification of deterministic classification ranges. |
| FR3 — DOE information retrieval and explanation | Missing topics and potential extraction errors may reduce answer quality. |
| FR4 — Source citations | Missing page references reduce citation precision and traceability. |
| NFR2 — Answer correctness (>=85%) | Incomplete or incorrectly extracted information may reduce correctness. |
| NFR3 — Recall@5 (>=85%) | Missing source content may reduce retrieval recall. |
| RAI1 — Source grounding / citation match (>=95%) | Incomplete evidence and provenance may reduce grounding and citation match. |
| RAI3 — Document metadata currency | Unverified dates and versions prevent confirmation of currency. |
| RAI4 — No storage of personal identifiers | Future data and user-input handling require privacy review. |

These are potential impacts, not measured system-level failures. Confirm IDs and thresholds against the final Topic 2 requirements and evaluate system performance in Topic 8.

## 8. Topic 4 Quality Gate Decision

**HOLD — for full downstream use of the corpus.**

The current dataset can be retained as evidence of Topic 4 quality assessment, but it is not ready for unrestricted downstream use. A selected authoritative source is missing, page metadata is incomplete, and reuse rights and factual extraction accuracy remain unverified.

Release conditions:

1. Include the DOE API TXT source and verify required topic coverage.
2. Recover page references and verify extracted text and numerical relationships.
3. Verify document currency and appropriate reuse permissions.
4. Rerun validation, deduplication and coverage checks on the updated corpus and record the results.

Owner: Project developer. Timing: before downstream corpus use; verify rights before redistribution. The HOLD decision is a proposed engineering judgement, not a lecturer-approved decision. Completion of the lab assessment itself does not imply that the corpus has passed the quality gate.
