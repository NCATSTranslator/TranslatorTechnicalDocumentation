[[architecture/kp/index|Back to KPs]]

## General Description
We developed the Genetics Knowledge Provider (KP), a knowledge-centric data provider for computation based genetic association results, 
as part of the NCATS Biomedical Data Translator (“Translator”). The Genetics KP aims to 
* integrate Genome Wide Association Studies (GWAS) data sources in an unbiased way.
* provide a curated, unified framework for genetic associations to deepen our understanding of gene/disease biology. 

The Genetics KP takes advantage of broad access to disease specific GWAS datasets, portals, and computational tools, 
to integrate information available for diseases and their associated genes, including similarity-based connections. We follow a stringent 
procedure to avoid expert bias, including data scouting and recording data provenance, to create a unified framework for gene/disease associations. 

We bring to the Translator project computational genetics expertise, and using signal aggregating algorithms and tools to combine genetic signals across GWAS studies.

## Team Members
* Jason Flannick - Principal Investigator and Team Lead
* Noel Burt -  Director, Operations and Development, Knowledge Portals
* Marc Duby (mduby@broadinstitute.org) - Principal Software Engineer - (_contact with questions_)
* Ryan Koesterer - Senior Computational Analyst
* Maria Costanzo - Manager, Knowledge Portals

## Genetics KP Translator Reasoner API
* https://genetics-kp.transltr.io/genetics_provider/trapi/v1.4/

## Description of Genetics KP’s data resources
* _Genebass_ 
  * Downloaded loss of function (LoF) gene/disease association data
  * https://app.genebass.org/
* _GenCC_ 
  * Curated gene/disease association statistics
  * https://thegencc.org/
* _ClinVar_	
  * https://www.ncbi.nlm.nih.gov/clinvar/
* _ClinGen_	
  * https://clinicalgenome.org/
* _GWAS Dataset List_ 
  * Downloaded and harmonized 200+ GWAS studies; data is used with Magma gene aggregation method
  * Studies mostly pertaining to metabolic and musculoskeletal diseases
  * https://hugeamp.org:8000/datasets.html

## Computational Tools
* _Magma_ - for Gene/Disease variant pvalue aggregation using GWAS 
  * https://ctg.cncr.nl/software/magma
* _HuGE Calculator_ - For calculating the probability a gene is associated to a disease using common and rare variants
  * https://hugeamp.org:8000/hugecalculator.html
* _PIGEAN_ - A framework for gene prioritization
  * https://www.kp4cd.org/index.php/node/1516

## Source Code
* _GeneticsKP_ https://github.com/broadinstitute/genetics-kp-dev

## External Documentation
* _Additional Genetics KP documentation in GitHub_ https://github.com/broadinstitute/genetics-kp-dev
* _Gene Level Meta Analysis Method_ https://hugeamp.org:8000/help.html?page=955
* _Calculating Gene/Disease Probability Method_ https://hugeamp.org:8000/help.html?page=961
* _Selecting and Processing of GWAS Datasets_ https://hugeamp.org:8000/help.html?page=935