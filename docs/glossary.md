# Translator Glossary of Terms

## Translator UI: Web interface to the Translator system
* Displays scored and ranked results and evidence, confidence, and provenance from the ARS
* Currently only supports a select set of templated queries
* Production instance is accessible at https://ui.transltr.io/ 

## ARS: Autonomous Relay System
* Functions as a central relay station between ARAs
* Broadcasts user queries to the ARAs and compiles responses

## ARA: Autonomous Relay Agent
* Function is to build upon the knowledge contributed by KPs by way of reasoning and inference and in response to user-defined queries
* ARAs also apply scoring-and-ranking algorithms to query results in order to assist with user interpretation and evaluation of answers

## KP: Knowledge Provider
* Contributes domain-specific, high-value information abstracted from one or more underlying “knowledge sources,” which may be “raw” data or information that has been abstracted from the data

## TRAPI: Translator Reasoner Application Programming Interface
* A standard HTTP protocol for transmitting queries and receiving answers across the Translator ecosystem, with both structured as graphs

## Biolink Model
* An open-source, graph-oriented data model and upper-level ontology or schema for integrating and semantically harmonizing across disparate knowledge sources

## SRI Services
* Key Translator Platform support services such as **Name Resolver** and **Node Normalizer** that have been developed by the Translator Standards and Reference Implementation component to support standardization across Translator components
