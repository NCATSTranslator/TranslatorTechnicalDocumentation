# Welcome to the Biomedical Data Translator - Developer Documentation Site

This is the primary "developer" software development documentation site for the [Biomedical Data Translator](https://ncats.nih.gov/translator) program, sponsored by the [National Center for Advancing Translational Sciences ("NCATS")](https://ncats.nih.gov).

## Background and History

The Biomedical Data Translator (‘Translator’) program was launched by the National Center for Advancing Translational Sciences (NCATS) in Fall of 2016. The vision of the Translator program is to accelerate translational science “through an informatics platform that enables interrogation of relationships across the full spectrum of data types” (Fecho et al. 2022). The goal is to build the infrastructure required to support and facilitate data-driven translational research on a large scale. The fundamental aim is to integrate as many datasets as possible, using a ‘knowledge graph’–based architecture, and allow them to be cross-queried and reasoned over by translational researchers. A fundamental tenet of the Translator program is open data, including open patient data, and open team science.

The Biomedical Data Translator Consortium was established roughly one year after launch and is working collaboratively to realize the vision of the Translator program. The Translator consortium is currently comprised of ~215 team members and 27 institutions. Of note, the program is funded primarily through a National Institutes of Health (NIH) Other Transaction Awards (OTA) mechanism, although an NIH contract was awarded recently to support development of a Translator user interface (UI).

An overview of the Translator timeline, in the context of key milestones and award funding, is depicted below.

![image](https://user-images.githubusercontent.com/26254388/174347625-c20cc7b1-134b-4a19-ab21-72c4ad4d2f89.png)

*Taken from Fecho et al. 2022, Supplementary Figure 1*

## Overview of Translator Architecture

In brief, the Translator system is comprised of five main components, shown in the diagram below (Fecho et al. 2022). Knowledge Providers (KPs) contribute domain-specific, high-value information abstracted from one or more underlying ‘knowledge sources’. Autonomous Relay Agents (ARAs) build upon the knowledge contributed by KPs by way of reasoning and inference across KPs. The Autonomous Relay System (ARS) functions as a central relay station, is managed by NCATS, and is intended to broadcast user queries to the broader Translator ecosystem. A UI is under development but intended to serve as a public user interface to the Translator system. Finally, a Standards and Reference Implementation (SRI) Component provides services and community-based collaboration guidance related to the development, adoption, and implementation of the standards needed to achieve the overall implementation goals of the Translator system.

![image](https://user-images.githubusercontent.com/26254388/174347804-0412fbd2-f61f-4573-8073-2408c3c41e15.png)

*Taken from Fecho et al. 2022, Figure 1*

## Example Use Case Application

This example use case application is intended to provide a high-level overview of how to translate a user question into a Translator Reasoner Standard API (TRAPI) query, execute a TRAPI query, and evaluate results. The specific use case question is what drugs treat chronic pain?

Shown below is the translation of that user question into a TRAPI query.

![image](https://user-images.githubusercontent.com/26254388/174348079-4bf2ff96-db8e-432e-ba5d-7c82475ec821.png)

*Taken from Fecho et al. 2022, Figure 2*

In response to the query, Translator provided answers that are known to be treatments for chronic pain such as ibuprofen. Translator also provided answers that are correct but not terribly interesting or necessarily aligned with user intent such as caffeine (an adjuvant included in certain pain medication). Also included among Translator answers to the example query are answers such as naltrexone, an opioid antagonist. In support of naltrexone, Translator provided evidence and provenance indicating that naltrexone indeed may be used to treat chronic pain, as highlighted below. Translator evidence and provenance included ranked answers with scores, primary and secondary data sources behind any assertions, PMIDs and links to abstracts, etc. 

This sort of serendipitous discovery, or unexpected insight, represents the type of scientific discovery that Translator aims to foster.

![image](https://user-images.githubusercontent.com/26254388/174348255-2ba2d8d3-8f0e-4678-a4d1-997e299b4a1b.png)

*Taken from Fecho et al. 2022, Figure 3*

Translator is currently being used to promote serendipitous discovery and augment human reasoning in a variety of disease spaces, including Fanconi anemia, systemic sclerosis, cystic fibrosis, Parkinson’s disease, and drug-induced liver injury.

## Summary of Key Technical Achievements

- **Common Queries**: TRAPI has been adopted as an API standard to support query across Translator components
- **Common Semantics**: Biolink Model (Unni et al. 2022) has been adopted as a standard upper-level ontology to support semantic harmonization across disparate ontologies and data/knowledge sources
- **Entity Resolution**: SRI Name Resolution and Node Normalization services provide entity resolution to harmonize across disparate vocabularies and identifier systems
- **Discoverability**: SmartAPI Registry provides a platform for discovering Translator tools and components, including metadata to explain what functionalities those services support

## Key Programmatic Priorities

- **Quality Metrics/Benchmarking**: Identify quality metrics/benchmarking to evaluate query answers and verify that the system is robust and bug-free
- **Long-term Sustainability**: Develop and implement a long-term sustainability plan to allow for continued development and maintenance of Translator, should NCATS lose programmatic support
- **Solid User Base**: Engage both software developers and scientific end users from outside of the Translator Consortium
- **Documentation**: Develop easy-to-understand documentation and tutorials to more readily engage outside collaborators
- **User Interface**: Create a user interface to promote user engagement (initial release expected September 2022)

## References

1.	Austin CP, Colvis, CM, Southall NT. Deconstructing the translational tower of babel. Clin Transl Sci 2019;12(2):85. doi: 10.1111/cts.12595. https://ascpt.onlinelibrary.wiley.com/doi/10.1111/cts.12595 
2.	The Biomedical Data Translator Consortium. Toward a universal biomedical data translator. Clin Transl Sci 2019a;12(2):91–94. doi: 10.1111/cts.12592. https://pubmed.ncbi.nlm.nih.gov/30412337/ 
3.	The Biomedical Data Translator Consortium. The Biomedical Data Translator program: conception, culture, and community. Clin Transl Sci 2019b;12(2):86–90. doi: 10.1111/cts.13021. https://pubmed.ncbi.nlm.nih.gov/30412340/ 
4.	Fecho K, Thessen AE, Baranzini SE, et al. and The Biomedical Data Translator Consortium. Progress toward a universal biomedical data translator. Clin Transl Sci, in press. doi: 10.1111/cts.13301. https://pubmed.ncbi.nlm.nih.gov/35611543/ 
5.	Unni DR, Moxon SAT, Bada M, et al. and the Biomedical Data Translator Consortium. Biolink model: a universal schema for knowledge graphs in clinical, biomedical, and translational science. Clin Transl Sci, in press. doi: 10.1111/cts.13302. https://ascpt.onlinelibrary.wiley.com/doi/full/10.1111/cts.13302 

## Overview of Technical Documentation

* [Architecture](architecture/index.md)
* [Guide for Developers](guide-for-developers)
* [About Translator](about/index.md)


## Joining the Translator Community as a Developer

* What are the mandatory technical requirements of having your stuff in Translator (Minimal standards; QA)
* How do keep quality assurance / gatekeeping in place; rubber stamping; governance; vetting process for new internal KP's etc.  - Governance issues?


## Other Developer Resources

* [Frequently Asked Questions (FAQ)](faq.md) (everyone)
