![image](img/translator-banner.jpg)

# Welcome to the Biomedical Data Translator - Technical Documentation Site 

This site hosts the official technical documentation for the Biomedical Data Translator ("Translator") program. Key sections of the documentation are:

- This overview page (and related links), presenting an overview of the Biomedical Data Translator consortium and its platform.
- [Knowledge Graphs](architecture/biolink/knowledge_graphs.md): Knowledge Graphs - the core scientific principle behind Translator.
- [Translator Architecture](architecture/index.md): overview of the Translator knowledge integration platform.
- [Software Development Guide](development-guide/index.md): guidelines for Translator software development, including tutorials.
- [System Deployment Guide](deployment-guide/index.md): guidelines for Translator systems administration, including continuous integration testing, production deployment and monitoring.

## Vision for the Translator Program

The vision for the Translator program is to accelerate translational science "_through an informatics platform that 
enables interrogation of relationships across the full spectrum of data types_"
([Austin _et al._ 2019](https://doi.org/10.1111/cts.12595), [BDTC 2019a](https://doi.org/10.1111/cts.12591),
[BDTC 2019b](https://doi.org/10.1111/cts.12592), [Fecho _et al._ 2022](https://doi.org/10.1111/cts.13301),
[other references](#references)). The goal is to build the infrastructure required to support and 
facilitate data-driven translational research on a large scale. The fundamental aim is to integrate as many datasets
as possible, using a ‘knowledge graph’–based architecture, and allow them to be cross-queried and reasoned over by
translational scientists in an effort to derive new insights and knowledge. A fundamental tenet of the Translator program is open data, including open (de-identified) 
patient data, and open team science.

## Overview of the Translator System

The Translator System is both federated and hierarchical. A schematic is provided on the architecture page. In brief, a user query's to the Translator user interface (UI) gets transmitted to the Translator "Autonomous Relay Service (ARS)", which then transmits the query in machine language to several Translor "Autonomous Relay Agents (ARAs)", who then transmit the machine-language query to numerous Translator "Knowledge Providers (KPs)", who then return their answers to the original query, in whole or in part, back to the ARAs, who then compile results and reason over them to derive answers to the user's original query, and then send them back to the ARS, which then merges for results from all ARAs, scores and ranks them, and adds annotations before returning the full result set back to the UI for user display and interrogation of the supporting evidence, confidence in results, and related provenance.

Translator currently supports four main types of queries, with full evidence, providence, and confidence returned with query results. Here, we provide a brief high-level overview of each query type, with details included in other sections.

1. "Lookup" queries refer to queries that ask Translator to essentially find "facts" or highly curated knowledge that typically take the form of a simple "one-hop" answer path. For instance, in response to a natural language query that asks "what drugs may treat asthma?", Translator may return an anser that states "albuterol treats asthma".
2. "Inferred" queries ask Translator to suggest an answer to a question that has varying degrees of confidence in the results. These inferences are derived from multiple reasoning algorithms and chains, including rule-based approaches, probabilistic models, and curated workflow paths that subject matter experts hypothesize as having the potential to derive novel results. "Inferred" queries can yield one-hop answer paths, but they are typically multi-hop answer paths. For example, in response to a natural language query that asks "what chemicals may increase the activity of the gene/protein SCN1A?", Translator might yield an inferred answer that suggests ranolazine, but in the form of an inferred answer path that states "ranolazine causes an increased activity or abundance of the gene/protein MTOR, which causes an increased activity or abundance of the gene/protein SCN1A".
3. "Pathfinder" queries ask Translator to find paths that connect two biomedical entities, for instance, a chemical exposure and an adverse outcome. Translator uses a variety of approaches, including combinations of "lookup" and "inferred" queries to derive answers to "pathfinder" queries. As such, these queries typically yield complex multi-hop answer paths. For instance, in natural language, a user might ask "what biological mechanisms might explain an observed relationship between exposure to polybrominated diphenyl ethers and cardiovascular disease?"
4. "Input_set" queries differ from the other types of queries in that users ask Translator to find a shared relationship between multiple user-contributed input entities (e.g., phenotypes) and another entity type (e.g., gene). This query functionality differs from a BATCH query, in which multiple input entities are entered by users, with Translator returning independent results for each input entity. The functionality also differs from an AND query, in which multiple input entities are entered by users, with Translator returning results for only those entities that are shared by all of the input entities. Rather, the "input_set" functionality operates more as an OR query, in which multiple input entities are entered by users, with Translator returning results for entities that are shared by some, but not all, of the input entities. For instance, a user may ask "what genes are related to one or more of these unusual and presumably unrelated phenotypes?"

Translator is currently being used to promote serendipitous discovery and augment human reasoning in a variety of
disease spaces, including Fanconi anemia, systemic sclerosis, cystic fibrosis, Parkinson’s disease, drug-induced liver injury, primary ciliary dyskinesia, cyclic vomiting syndrome, and many others. (Please see the abbreviated References list for additional examples and details.)

Translational scientists can access Translator via the [Translator UI](https://ui.transltr.io/). Additionally, developers or anyone with skills in Python can try out the [“Hello Translator” Jupyter Notebook](development-guide/HelloTranslator.ipynb). 

## About the Translator Program

The [**Biomedical Data Translator**](https://ncats.nih.gov/translator)  program was launched by the
[National Center for Advancing Translational Sciences ("NCATS")](https://ncats.nih.gov) in Fall of 2016. ([Austin et al. 2019; BDTC 2919a/b;
Fecho _et al._ 2022; Unni _et al._  2022](index.md#references)). The **Biomedical Data Translator ("Translator") Consortium** 
is working collaboratively to realize the vision of the Translator program. 

Phase 2 "Development" focused activities of the **Translator Consortium** engaged [~215 team members and 27 institutions](https://github.com/NCATSTranslator/Translator-All/wiki). 

The program is [funded primarily through a National Institutes of Health (NIH) Other Transaction Awards (OTA) mechanism and an NIH contract awarded to support development of a Translator user interface (UI)](#consortium-funding).

### Key Programmatic Priorities

- **Quality Metrics/Benchmarking**: Identify quality metrics/benchmarking to evaluate query answers and verify that the system is robust and bug-free
- **Long-term Sustainability**: Develop and implement a long-term sustainability plan to allow for continued development and maintenance of Translator, should NCATS lose programmatic support
- **Solid User Base**: Engage both software developers and scientific end users from outside of the Translator Consortium
- **Documentation**: Develop easy-to-understand documentation and tutorials to more readily engage outside collaborators
- **User Interface**: Create a user interface to promote user engagement (initial release expected September 2022)

### Key Technical Achievements

- **Common Semantics**: the Consortium's inspired Biolink Model ([Unni _et al._ 2022](index.md#references)) has been adopted as a standard data model and upper-level ontology to support semantic harmonization across disparate ontologies and data/knowledge sources
- **Entity Resolution**: the Consortium's Standards & Reference Implementation ("SRI") team-implemented Name Resolution and Node Normalization services provide entity resolution to harmonize across disparate vocabularies and identifier systems
- **Common Queries**: the Consortium's OpenAPI-based Translator Reasoner Application Programming Interface ("TRAPI") has been adopted as an API standard to support query across Translator components
- **Discoverability**: the Consortium's support for the SmartAPI Registry provides a platform for discovering Translator tools and components, including metadata to explain what functionalities those components or services support

### Consortium Funding

**Translator Phase 2 'Development' funding:** NCATS Intramural Funding ZIA TR000276-05; NCATS Contract #75N95021P00636; Health & Human Services OT2TR003434; OT2TR003436; OT2TR003430; OT2TR003433; OT2TR003437; OT2TR003443; OT2TR003445; OT2TR003422; OT2TR003441; OT2TR003450; OT2TR003428; OT2TR003448; OT2TR003427; OT2TR003435; OT2TR003449

**Translator Phase 1 'Feasibility' funding:** OT3TR002026, OT3TR002020, OT3TR002025, OT3TR002019, OT3TR002027, OT2TR002517, OT2TR002514, OT2TR002515, OT2TR002584, OT2TR002520.

###  Licensing

The Translator Consortium makes every effort to draw only from openly available, public datasets. The Translator program's leadership also has brokered licensing agreements with certain data owners such as DrugBank. Note, however, that the system components developed by different Translator teams may have other distinct specific licensing. 

**_This_** document repository is published under the [Creative Commons CC0 1.0 Universal License](license.md)

### References

1. Austin CP, Colvis, CM, Southall NT. **Deconstructing the Translational Tower of Babel.** _Clin Transl Sci_, 2019;12(2):85. [doi:10.1111/cts.12595](https://doi.org/10.1111/cts.12595). [PMID:30412342](https://pubmed.ncbi.nlm.nih.gov/30412342/).
2. The Biomedical Data Translator Consortium. **Toward a Universal Biomedical Data Translator.** _Clin Transl Sci_, 2019a. [doi:10.1111/cts.12591](https://doi.org/10.1111/cts.12591). [PMID:30412337](https://pubmed.ncbi.nlm.nih.gov/30412337/).
3. The Biomedical Data Translator Consortium. **The Biomedical Data Translator program: conception, culture, and community.** _Clin Transl Sci_, 2019b. [doi:10.1111/cts.12592](https://doi.org/10.1111/cts.12592). [PMID:30412340](https://pubmed.ncbi.nlm.nih.gov/30412340/).
4. Fecho K, Thessen AE, Baranzini SE, et al. and The Biomedical Data Translator Consortium. **Progress toward a Universal Biomedical Data Translator.** _Clin Transl Sci_, 2022 May 25. [doi:10.1111/cts.13301](https://doi.org/10.1111/cts.13301). [PMID:35611543](https://pubmed.ncbi.nlm.nih.gov/35611543/).
5. Unni DR, Moxon SAT, Bada M, et al. and the Biomedical Data Translator Consortium. **Biolink Model: a universal schema for knowledge graphs in clinical, biomedical, and translational science.** _Clin Transl Sci_, 2022 June 6. [doi:10.1111/cts.13302](https://doi.org/10.1111/cts.13302).
