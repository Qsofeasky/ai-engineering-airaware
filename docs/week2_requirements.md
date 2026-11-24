# AirAware AI — Week 2 Requirements

## Functional Requirements

| # | Requirement — The system SHALL | Scope Boundary — SHALL NOT (where relevant) |
| --- | --- | --- |
| FR1 | Accept English-language questions about Malaysian air quality through a web interface. | Answer unrelated general-purpose questions. |
| FR2 | Classify a user-provided numerical API reading according to official Malaysian API categories and explain the category. | Claim that the reading represents current local air quality without a verified live source. |
| FR3 | Retrieve relevant information from approved environmental documents and generate understandable explanations. | Invent facts that are unsupported by the retrieved sources. |
| FR4 | Provide verifiable document references for source-based answers. | Present unsupported information as official DOE guidance. |
| FR5 | Inform users when a question cannot be answered using available documents and redirect out-of-scope requests appropriately. | The system shall not generate answers when sufficient supporting information is unavailable. |

## Non-Functional Requirements

| # | Quality Attribute | Requirement | Measurement Method | Metric | Threshold |
| --- | --- | --- | --- | --- | --- |
| NFR1 | Performance | The system shall respond within an acceptable time. | Measure 100 queries on the target test environment. | 90th percentile response latency | ≤ 5 seconds |
| NFR2 | Correctness | Answers shall be factually consistent with approved documents. | Score a labelled question set against reference answers. | Correct response rate | ≥ 85% |
| NFR3 | Retrieval Quality | The system shall retrieve relevant passages for supported questions. | Compare top-five retrieved passages with manually labelled relevant passages. | Recall@5 | ≥ 85% |
| NFR4 | Maintainability | Approved source updates shall be incorporated without rebuilding the whole application. | Conduct a controlled document replacement and indexing test. | Document update time | ≤ 10 minutes |

## Responsible AI Requirements

| # | Responsible AI Risk | Requirement | Measurement Method | Metric | Threshold |
| --- | --- | --- | --- | --- | --- |
| RAI1 | Hallucination/Grounding | The system shall provide verifiable citations for document-based answers. | Check citations against source passages. | Citation presence and citation-source match | 100% presence; ≥ 95% match |
| RAI2 | Safety/ scope | The system shall refuse or redirect unsupported medical, forecasting and other out-of-scope requests. | Test at least 20 out-of-scope questions. | Correct refusal-and-redirect rate | ≥ 95% |
| RAI3 | Outdated Information | The system shall display source identification and document dates where available. | Audit responses against the document registry. | Correct source metadata rate | 100% |
| RAI4 | Privacy | The system shall not persist personal identifiers entered in user questions. | Inspect application logs and saved records using synthetic identifiers. | Persisted test identifiers | 0 |

## Part A Reflection

The most difficult Responsible AI requirement to measure is RAI1, hallucination and source grounding. A response may sound correct while containing information not supported by the retrieved documents. Therefore, manual checking against official sources is needed to determine whether citations genuinely support the generated explanations.
