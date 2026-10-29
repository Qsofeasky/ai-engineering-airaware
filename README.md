AirAware AI

AI-Based Air Quality Information and Guidance System

AirAware AI is a web-based AI assistant that helps Malaysians understand air pollution information using official environmental documents.

The system uses Natural Language Processing (NLP), semantic retrieval, and Retrieval-Augmented Generation (RAG) to answer questions about air quality.

Problem Statement

Although Malaysia provides air quality information through the Department of Environment (DOE) and APIMS, some users may find it difficult to interpret API readings and understand technical environmental information.

AirAware AI aims to make this information easier to understand by retrieving relevant information from official documents and generating clear explanations with supporting references.

Evidence of the Problem

The DOE provides API readings and classifications, but users may still have questions about their meaning.

Official air quality standards contain technical information about pollutants and concentration limits that may be difficult for non-experts to interpret.

These observations motivate the proposed system. Further evidence will be collected to establish the extent of the problem.

Initial Related Work / Existing Approaches

APIMS: Provides air quality readings and classifications but is not primarily a conversational information assistant.

DOE Environmental Documents: Provide official technical information but require users to locate and interpret relevant sections.

Traditional Keyword Search: Retrieves information based on matching terms but may perform less effectively when questions use different wording.

Engineering Gap / Limitation

Existing air quality information sources may require users to manually search and interpret technical information.

AirAware AI proposes a document-grounded conversational interface that combines semantic retrieval with RAG to provide understandable explanations supported by official sources.

Project Objectives

O1: To design an AI-based air quality information system using official Malaysian environmental documents.

O2: To develop a web-based AI assistant using semantic retrieval and RAG.

O3: To evaluate retrieval relevance, answer accuracy, citation correctness, and response time.

Target Users

Malaysian residents, especially students, outdoor workers, and members of the public seeking air quality information.

Data Sources

Source 1: New Malaysia Ambient Air Quality Standard

Department of Environment Malaysia.
https://www.doe.gov.my/wp-content/uploads/2021/10/Air-Quality-Standard-BI.pdf

Contains information about air pollutants, concentration limits, and averaging periods.

Source 2: Air Pollutant Index (API) Information

Department of Environment Malaysia.
https://www.doe.gov.my/2021/10/04/english-air-pollutant-index-api/

Provides information about API classifications and interpretation.

Source 3: Environmental Quality (Clean Air) Regulations 2014

Department of Environment Malaysia.
https://eswis.doe.gov.my/helpDocs/No.5%20-%202014/Peraturan-peraturan_kualiti_alam_sekeliling_udara_bersih_2014_EN.pdf

Optional source covering industrial air pollution regulations.
