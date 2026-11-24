# AirAware AI — Week 2 Architecture Decisions

## C2 — Requirements-to-Architecture Mapping

| Requirement ID | What does the requirement need? | Architecture Response |
| --- | --- | --- |
| FR3 | Retrieve relevant information from official environmental documents and provide understandable explanations. | Semantic Retrieval and RAG Answer Generation retrieve relevant passages and generate source-grounded answers. |
| FR4 / RAI1 | Provide verifiable citations and reduce unsupported AI-generated information. | Citation and Evidence Check verifies whether generated explanations are supported by retrieved documents. |
| FR5 / RAI2 | Identify questions outside the project scope and avoid unsafe or unsupported answers. | Scope and Safety Control checks user queries before processing and returns appropriate responses when necessary. |

## C4 — Architecture Decisions and Trade-offs

| Decision | Requirement / Constraint | Alternatives Considered | Selected Option | Trade-off Accepted |
| --- | --- | --- | --- | --- |
| Include knowledge retrieval | Answers must be based on official environmental documents (FR3, RAI1). | Base AI model only, keyword search and semantic retrieval. | Semantic Retrieval with RAG | More processing complexity, but better access to relevant information and source grounding. |
| Include scope and safety control | Unsupported or out-of-scope questions must be handled appropriately (FR5, RAI2). | Prompt instructions only and explicit scope checking. | Explicit Scope and Safety Control | May incorrectly reject some valid questions, but improves safety. |
| Include citation verification | Generated explanations must include verifiable source references (FR4, RAI1). | Display citations and evidence verification. | Citation and Evidence Check | Additional processing time, but improves answer reliability and traceability. |

## C4 — Initial Requirements Traceability Matrix

| Objective | Requirement | Evaluation Criterion | Architecture Element | Later Evidence |
| --- | --- | --- | --- | --- |
| O1: Design a document-grounded AI air quality assistant. | FR3 , NFR3 | Retrieval relevance (Recall@5 ≥ 85%). | Semantic Retrieval and Official DOE Document Repository | Retrieval evaluation results using prepared test questions. |
| O2: Develop a web-based assistant that provides understandable, source-supported explanations. | FR1, FR4, RAI1 | Answer correctness ≥ 85%; citation-source match ≥ 95%. | Web Application, RAG Answer Generation, Citation and Evidence Check | Answer evaluation results and citation verification records. |
| O3: Evaluate system reliability, safety, and performance. | FR5, NFR1, RAI2 | 95% correct handling of out-of-scope questions; p90 response time ≤ 5 seconds. | Scope and Safety Control, Query Processing, Evaluation and Monitoring | Safety test results and response-time measurements. |

## C4 Reflection

The most important trade-off was choosing Semantic Retrieval with RAG instead of relying only on a base AI model. This decision was driven by FR3 and RAI1, which require accurate, source-grounded explanations from official environmental documents. The accepted trade-off was increased system complexity and processing time in exchange for better answer reliability and traceability.
