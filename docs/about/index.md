![image](../img/translator-banner.jpg)

# About Translator

The **Biomedical Data Translator** (‘Translator’) program was launched by the National Center for
Advancing Translational Sciences (NCATS) in Fall of 2016 ([Austin et al. 2019; BDTC 2919a/b;
Fecho _et al._ 2022; Unni _et al._  2022](#references)). The **Biomedical Data Translator Consortium**
was established roughly one year after launch and is working collaboratively to realize the vision of the
Translator program. The Translator consortium is currently comprised of ~215 team members and 27 institutions.
Of note, the program is funded primarily through a National Institutes of Health (NIH) Other Transaction Awards (OTA)
mechanism, although an NIH contract was awarded recently to support development of a Translator user interface (UI).

An overview of the Translator timeline, in the context of key milestones and award funding, is depicted below.

![image](https://user-images.githubusercontent.com/26254388/174347625-c20cc7b1-134b-4a19-ab21-72c4ad4d2f89.png)

Taken from Fecho _et al._ 2022, Supplementary Figure 1

Translator is currently being used to promote serendipitous discovery and augment human reasoning in a variety of
disease spaces, including Fanconi anemia, systemic sclerosis, cystic fibrosis, Parkinson’s disease,
and drug-induced liver injury.

## Summary of Key Technical Achievements

- **Common Queries**: TRAPI has been adopted as an API standard to support query across Translator components
- **Common Semantics**: Biolink Model (Unni _et al._ 2022) has been adopted as a standard upper-level ontology to support semantic harmonization across disparate ontologies and data/knowledge sources
- **Entity Resolution**: SRI Name Resolution and Node Normalization services provide entity resolution to harmonize across disparate vocabularies and identifier systems
- **Discoverability**: SmartAPI Registry provides a platform for discovering Translator tools and components, including metadata to explain what functionalities those services support

## Key Programmatic Priorities

- **Quality Metrics/Benchmarking**: Identify quality metrics/benchmarking to evaluate query answers and verify that the system is robust and bug-free
- **Long-term Sustainability**: Develop and implement a long-term sustainability plan to allow for continued development and maintenance of Translator, should NCATS lose programmatic support
- **Solid User Base**: Engage both software developers and scientific end users from outside of the Translator Consortium
- **Documentation**: Develop easy-to-understand documentation and tutorials to more readily engage outside collaborators
- **User Interface**: Create a user interface to promote user engagement (initial release expected September 2022)

## References

1. Austin CP, Colvis, CM, Southall NT. **Deconstructing the Translational Tower of Babel.** _Clin Transl Sci_, 2019;12(2):85. [doi:10.1111/cts.12595](https://ascpt.onlinelibrary.wiley.com/doi/10.1111/cts.12595). [PMID:30412342](https://pubmed.ncbi.nlm.nih.gov/30412342/).
2. The Biomedical Data Translator Consortium (BDTC). **Toward a Universal Biomedical Data Translator.** _Clin Transl Sci_, 2019a;12(2):91–94. [doi:10.1111/cts.12592](https://ascpt.onlinelibrary.wiley.com/doi/full/10.1111/cts.12592). [PMID:30412337](https://pubmed.ncbi.nlm.nih.gov/30412337/).
3. BDTC. **The Biomedical Data Translator program: conception, culture, and community.** _Clin Transl Sci_, 2019b;12(2):86–90. doi: 10.1111/cts.13021. [PMID:30412340](https://pubmed.ncbi.nlm.nih.gov/30412340/).
4. Fecho K, Thessen AE, Baranzini SE, et al. and The Biomedical Data Translator Consortium. **Progress toward a Universal Biomedical Data Translator.** _Clin Transl Sci_, 25 May 2022. [doi:10.1111/cts.13301](https://ascpt.onlinelibrary.wiley.com/doi/full/10.1111/cts.13301). [PMID:35611543](https://pubmed.ncbi.nlm.nih.gov/35611543/).
5. Unni DR, Moxon SAT, Bada M, et al. and the Biomedical Data Translator Consortium. **Biolink Model: a universal schema for knowledge graphs in clinical, biomedical, and translational science.** _Clin Transl Sci_, 06 June 2022. [doi:10.1111/cts.13302](https://ascpt.onlinelibrary.wiley.com/doi/full/10.1111/cts.13302).

##  Licensing

Translator is intended to evolve into a global public good through open source and access licensing. In this spirit, this document repository is  published under the [CC0 1.0 Universal License](license.md)

## Consortium Teams (June 2022)

- **NCATS Project Management:** Link Brokers
- **Standards and Technical Coordination:** [Standards & Reference Implementation Team](../architecture/sri.md)
- [**User Interface Team**](../architecture/ui.md)
- [**Autonomous Relay Agents:**](../architecture/ara.md)
  - Ranking Agent
  - imProving Agent
  - Unsecret Agent
  - Explanatory Agent
  - Expander Agent
  - Exploring Agent
- [**Knowledge Providers:**](../architecture/kp.md)
  - Service Provider
  - Multiomics Provider
  - Clinical Data Provider
  - Connections Hypothesis Provider
  - Molecular Data Provider
  - Text Mining Provider
  - Exposures Provider
  - Genetics Provider
