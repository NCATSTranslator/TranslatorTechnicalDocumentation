![image](../img/translator-banner.jpg)

# Guide for Developers

This section of the Technical Documentation provides several resources for developers designing, implementing and maintaining Translator software.  

- [Quick Start](quickstart.md)
- **Graph Modeling Paradigms:**
    - [Core knowledge graph principles](../architecture/biolink/knowledge_graphs.md)
    - [Key Biolink Model components](https://biolink.github.io/biolink-model/guidelines/understanding-the-model.html)
    - [Getting started with Biolink](https://biolink.github.io/biolink-model/guidelines/using-the-modeling-language.html)
    - [Working with the model (tutorial)](https://biolink.github.io/biolink-model/guidelines/working-with-the-model.html)
- [Developer Cookbook](cookbook.md)
- [Tutorials](tutorials/index.md)
- [Testing Resources](../architecture/sri/testing/index.md)
- [Frequently Asked Questions (FAQ)](../faq.md)

The actual deployment of the system is further documented in the [Deployment Guide](../deployment-guide/index.md).

An overview of the Translator Architecture is provided in the [Architecture overview page](index.md).  
Briefly, the system is composed of the following components:

1. [User Interface (UI)](../architecture/ui.md)
2. [Autonomous Relay System (ARS)](../architecture/ars_usage.md)
3. [Workflow Runner](../architecture/workflows.md)
4. [Translator Reasoner Application Programming Interface (TRAPI)](../architecture/sri/trapi.md)
5. [Translator SmartAPI Registry](../architecture/registry.md)
6. [Autonomous Relay Agents (ARAs)](../architecture/ara/index.md)
7. [Knowledge Providers (KPs)](../architecture/kp/index.md)

Tying together the above components are the activities, standards and service components of the Translator
[Standards and Reference Implementation ("SRI")](../architecture/sri/index.md) project team.

Additional architecture details are stored in the
[Translator Architecture repository](https://github.com/NCATSTranslator/TranslatorArchitecture).

## Joining the Translator Community as a Developer [draft]

* What are the mandatory technical requirements of having your stuff in Translator (Minimal standards; QA)
* How do keep quality assurance / gatekeeping in place; rubber-stamping; governance; vetting process for new internal KP's etc.  - Governance issues?
