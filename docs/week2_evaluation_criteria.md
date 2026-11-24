# AirAware AI — Week 2 Evaluation Criteria

## Evaluation Criteria

| Objective / Requirement ID | Evaluation Criterion | Capability Bucket | Measurement Method | Metric | Threshold | User / Business Outcome |
| --- | --- | --- | --- | --- | --- | --- |
| O3 / NFR 2 | Answer correctness | Domain- specific | Compare responses with prepared reference answers. | Correct response rate | ≥ 85% | Users receive reliable information. |
| O2 / NFR 3 | Retrieval relevance | Domain – specific | Evaluate the top five retrieved passages against labelled evidence. | Recall@5 | ≥ 85% | Relevant information can be found. |
| O2 / FR4 / RAI 1 | Citation Support | Instruction following | Inspect citations and verify source support. | Citation presence; match rate | 100%; ≥ 95% | Users can verify explanations. |
| O2 / RAI 2 | Out-of-scoper handling | Instruction following | Test 20 unsupported or unsafe queries. | Refusal-and-redirect success rate | ≥ 95% | Users are less likely to receive inappropriate guidance. |
| O3 / NFR 1 | Response latency | Cost and latency | Measure 100 queries. | p90 response time | ≤ 5 seconds | Users receive timely answers. |
| O2 / FR 3 | Explaination clarity | Generation | Human reviewers score answers using a 1–5 clarity rubric. | Mean clarity score | ≥ 4/5 | Non-experts can understand the information. |

## Part B Reflection

Answer correctness is the most important evaluation criterion because AirAware AI is intended to provide reliable environmental information. Incorrect explanations could cause users to misunderstand air pollution conditions. Therefore, answers must be checked against official environmental documents.
