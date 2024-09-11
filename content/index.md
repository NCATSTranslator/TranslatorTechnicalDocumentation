---
title: Home
---
![[img/translator-banner.jpg|image]]

# Welcome to the Biomedical Data Translator - Technical Documentation Site 
The vision of the Biomedical Data Translator ("Translator") program is to accelerate translational science "_through an informatics platform that 
enables interrogation of relationships across the full spectrum of data types_"
([Austin _et al._ 2019](https://doi.org/10.1111/cts.12595), [BDTC 2019a](https://doi.org/10.1111/cts.12591),
[BDTC 2019b](https://doi.org/10.1111/cts.12592), [Fecho _et al._ 2022](https://doi.org/10.1111/cts.13301),
[other references](#references)). The goal is to build the infrastructure required to support and 
facilitate data-driven translational research on a large scale. The fundamental aim is to integrate as many datasets
as possible, using a ‘knowledge graph’–based architecture, and allow them to be cross-queried and reasoned over by
translational researchers. A fundamental tenet of the Translator program is open data, including open (de-identified) 
patient data, and open team science.

- This overview page (and related links), presenting an overview of the Biomedical Data Translator consortium and its platform.
- [[Knowledge Graphs]]: Knowledge Graphs - the core scientific principle behind Translator.
- [Translator Architecture](architecture/index.md): overview of the Translator knowledge integration platform.
- [Software Development Guide](development-guide/index.md): guidelines for Translator software development, including tutorials.
- [System Deployment Guide](deployment-guide/index.md): guidelines for Translator systems administration, including continuous integration testing, production deployment and monitoring.

## About the Biomedical Data Translator

The [**Biomedical Data Translator**](https://ncats.nih.gov/translator)  program was launched by the
[National Center for Advancing Translational Sciences ("NCATS")](https://ncats.nih.gov) in Fall of 2016. ([Austin et al. 2019; BDTC 2919a/b;
Fecho _et al._ 2022; Unni _et al._  2022](index.md#references)). The **Biomedical Data Translator ("Translator") Consortium** 
is working collaboratively to realize the vision of the Translator program. 

The **Translator Consortium** is currently comprised of [~215 team members and 27 institutions](teams/index.md). The program is [funded primarily through a National Institutes of Health (NIH) Other Transaction Awards (OTA) mechanism and an NIH contract awarded to support development of a Translator user interface (UI)](#consortium-funding).

An overview of the Translator timeline, in the context of key milestones and award funding from program inception through September 2022, is depicted below.

![image](https://user-images.githubusercontent.com/26254388/174347625-c20cc7b1-134b-4a19-ab21-72c4ad4d2f89.png)

Taken from Fecho _et al._ 2022, Supplementary Figure 1

Translator is currently being used to promote serendipitous discovery and augment human reasoning in a variety of
disease spaces, including Fanconi anemia, systemic sclerosis, cystic fibrosis, Parkinson’s disease,
drug-induced liver injury, and many others.

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

**Translator Phase 2 'Development' funding:** NCATS Intramural Funding ZIA TR000276-05; NCATS Contract <label>#</label>75N95021P00636; Health & Human Services OT2TR003434; OT2TR003436; OT2TR003430; OT2TR003433; OT2TR003437; OT2TR003443; OT2TR003445; OT2TR003422; OT2TR003441; OT2TR003450; OT2TR003428; OT2TR003448; OT2TR003427; OT2TR003435; OT2TR003449

**Translator Phase 1 'Feasibility' funding:** OT3TR002026, OT3TR002020, OT3TR002025, OT3TR002019, OT3TR002027, OT2TR002517, OT2TR002514, OT2TR002515, OT2TR002584, OT2TR002520.

##  Licensing

Translator is intended to evolve into a global public good through open source and access licensing.

In this spirit, **_this_** document repository is  published under the [[License|Creative Commons CC0 1.0 Universal License]]

Note, however, that the system components developed by different Translator teams may have other distinct specific licensing. 

### References

1. Austin CP, Colvis, CM, Southall NT. **Deconstructing the Translational Tower of Babel.** _Clin Transl Sci_, 2019;12(2):85. [doi:10.1111/cts.12595](https://doi.org/10.1111/cts.12595). [PMID:30412342](https://pubmed.ncbi.nlm.nih.gov/30412342/).
2. The Biomedical Data Translator Consortium. **Toward a Universal Biomedical Data Translator.** _Clin Transl Sci_, 2019a. [doi:10.1111/cts.12591](https://doi.org/10.1111/cts.12591). [PMID:30412337](https://pubmed.ncbi.nlm.nih.gov/30412337/).
3. The Biomedical Data Translator Consortium. **The Biomedical Data Translator program: conception, culture, and community.** _Clin Transl Sci_, 2019b. [doi:10.1111/cts.12592](https://doi.org/10.1111/cts.12592). [PMID:30412340](https://pubmed.ncbi.nlm.nih.gov/30412340/).
4. Fecho K, Thessen AE, Baranzini SE, et al. and The Biomedical Data Translator Consortium. **Progress toward a Universal Biomedical Data Translator.** _Clin Transl Sci_, 2022 May 25. [doi:10.1111/cts.13301](https://doi.org/10.1111/cts.13301). [PMID:35611543](https://pubmed.ncbi.nlm.nih.gov/35611543/).
5. Unni DR, Moxon SAT, Bada M, et al. and the Biomedical Data Translator Consortium. **Biolink Model: a universal schema for knowledge graphs in clinical, biomedical, and translational science.** _Clin Transl Sci_, 2022 June 6. [doi:10.1111/cts.13302](https://doi.org/10.1111/cts.13302).
