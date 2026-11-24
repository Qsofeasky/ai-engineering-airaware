# Week 3 Data Inventory — AirAware AI

## Table 1: Requirements-to-Data Mapping

| Requirement ID | Needed information / feature | Candidate source | Why usable / constraint |
|---|---|---|---|
| FR2 | Official API categories and classification ranges | DOE Air Pollutant Index information | Official classification information; must preserve correct ranges. Verify category values against the original figure or official guidance. |
| FR3 | Air pollutant information and environmental standards for RAG explanations | DOE New Malaysia Ambient Air Quality Standard | Authoritative document; PDF text must be extracted and cleaned. |
| FR4 / RAI1 | Source information to support citations and reduce hallucinations | Both DOE sources | Preserve source title, URL, and document location. |
| NFR3 | Relevant text chunks for semantic retrieval | Both DOE sources | Chunk quality affects future retrieval performance. |

## Table 2: Source Inventory

| Field | Source 1 | Source 2 |
|---|---|---|
| Source name | New Malaysia Ambient Air Quality Standard | DOE Air Pollutant Index information |
| Owner | Department of Environment Malaysia | Department of Environment Malaysia |
| Format | PDF | Web page, converted to TXT |
| Data type | Unstructured text | Unstructured text |
| Purpose | Environmental standards and pollutant information | API categories and interpretation |
| Access | Public DOE website | Public DOE website |
| Usage rights | Verify reuse conditions | Verify reuse conditions |
| Data quality | Record actual PDF extraction findings | Record actual TXT inspection findings |
| Limitation | Tables may lose structure during extraction | Web content may change over time; figures may not be included in TXT extraction |
| Provenance | Original URL and source filename | Original URL and saved extraction date |
| Source URL | https://www.doe.gov.my/wp-content/uploads/2021/10/Air-Quality-Standard-BI.pdf | https://www.doe.gov.my/2021/10/04/english-air-pollutant-index-api/ |
| Local filename | `Air-Quality-Standard-BI.pdf` | `doe_api_information.txt` |

## Inspection Notes

After running the Colab inspection, record the actual number of PDF pages, whether text extraction succeeded, whether tables were preserved, whether the TXT file contains the API ranges, and any missing figure information. Do not mark these checks as completed before inspecting the files.

## Selected Data Preparation Method

The AirAware AI project uses Pathway A (PDF/TXT)
because both selected DOE sources contain
unstructured textual information.

The PDF source will be processed using text
extraction, cleaning, and paragraph-aware chunking.

The DOE API webpage has been converted into a TXT
file, which will be cleaned and divided into
smaller text chunks.

The prepared data will be saved in JSONL format
with source metadata to support semantic retrieval,
RAG explanations, and source citations.

Other pathways (CSV/Excel, images, JSON/API,
audio, and time-series) are not required for
the current project scope.
