[Back to KPs](index.md)

# Connections Hypothesis Provider

## Introduction
Connections Hypothesis Provider (CHP) is a collaborative service developed by Dartmouth College and Tufts University, in partnership with the National Center for Advancing Translational Sciences (NCATS). CHP's mission is to utilize clinical data and structured biochemical knowledge to create computational representations of pathway structures and molecular components. This effort supports both human and machine-driven analysis, enabling pathway-based biomarker discovery and contributing to the drug development process.

Currently, CHP serves as a platform for Gene Regulatory Network (GRN) discovery, allowing researchers to upload their own RNASeq data, or work with pre-existing datasets. Users can analyze, refine, and explore novel gene-to-gene regulatory relationships through our core discovery tool, GenNIFER, a web-based portal featuring state-of-the-art GRN inferencing algorithms. Additionally, the platform integrates with the Translator ecosystem, allowing users to contextualize their findings using existing knowledge sources.

Through its integration with the [Knowledge Collaboratory](https://github.com/MaastrichtU-IDS/knowledge-collaboratory) team, GenNIFER also enables researchers to publish their findings back into the Translator ecosystem, facilitating further collaboration and discovery.

Our team's specific tooling along with their respective repositories can be found here:
* [CHP API](https://github.com/di2ag/chp_api/tree/production): our central API service for interacting with CHP knowledge.
* [GenNIFER](https://github.com/di2ag/gennifer): our tool for GRN discovery.
* [Tissue-Gene Specificity Tool](https://github.com/di2ag/gene-specificity): our tool for assessing a gene’s expression specificity to a tissue.

For more information about our services or instructions on how to interact with our knowledge, please visit our [SmartAPI](http://smart-api.info/registry?q=412af63e15b73e5a30778aac84ce313f) page or refer to the [CHP API](https://github.com/di2ag/chp_api/tree/production) repository.

## Team Members:
Eugene Santos Jr - PI (Dartmouth)

Joseph Gormley – Co PI (Tufts)

Eugene Hinderer – Bioinformaticist (Tufts)

Tom Zisk – Developer (Tufts)

Dan Corkill – AI Research Scientist (Tufts)

Keumjoo Kim – Researcher (Dartmouth)

Gregory Hyde – Graduate Assistant (Dartmouth)

Anthony Ragazzi - Graduate Assistant (Dartmouth)

## Team Contacts:
Dr. Eugene Santos (PI): Eugene.Santos.Jr@dartmouth.edu

Joseph Gormley (Co-PI): jgormley@tuftsmedicalcenter.org

# TRAPI and Biolink
Trapi = 1.5.0

Biolink = 4.2.0

# Data Sources
[Genotype-Tissue Expression (GTEx) project]( https://www.gtexportal.org/home/)

[Genomic Data Commons (GDC)](https://portal.gdc.cancer.gov/)