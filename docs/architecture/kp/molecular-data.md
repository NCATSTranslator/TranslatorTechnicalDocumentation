[**Back to Home**](https://github.com/NCATSTranslator/NCATSTranslator.github.io/wiki)

# Molecular Data Provider (KP)

## General Description
The Molecular Data Provider, known as MolePro, is part of the NCATS Biomedical Data Translator project. MolePro integrates diverse chemical biology data sources and provides a curated framework for chemical entities, enhancing our understanding of their effects on biological targets.

Key features of MolePro include:

1. **Data Integration**: MolePro consolidates information from various public chemical biology datasets, portals, and tools to offer comprehensive insights into compounds and their protein targets. This includes similarity-based connections.

2. **Unbiased Approach**: We adhere to a stringent policy to avoid expert bias, ensuring true innovation. Our process involves impartial data scouting, efficient architecture building, and meticulous data provenance capturing.

3. **Unified Framework**: The result is a cohesive framework for compounds and targets, facilitating the identification of new compounds or targets through "guilt-by-association" inferences from large datasets.

4. **Chemical Biology Expertise**: MolePro contributes to the Translator project with expertise with probes in drug-discovery, toxicity flagging, and small-molecule mechanism of action elucidation.

MolePro harnesses powerful and diverse datasets to support research and development in chemical biology, ultimately aiming to deepen our understanding and application of chemical entities in biomedical science.

## Team Contact:

translator@broadinstitute.org

Vlado Dancik ([@vdancik](https://github.com/vdancik))

# Interfaces
MolePro was designed to provide the same molecular data knowledge in a choice of two APIs to cater to various user preferences: the MolePro API and the TRAPI.

### MolePro API
We have made MolePro's knowledge graph accessible to the scientific community through the MolePro API hosted on two servers:
* NCATS Translator server: https://molepro.transltr.io/molecular_data_provider/api
* Broad Institute server: https://translator.broadinstitute.org/molecular_data_provider/api

### Translator Reasoner API

MolePro can communicate biomedical questions and answers using the standardized Translator Reasoner API (TRAPI). Adhering to the TRAPI standard, MolePro integrates the query graph, knowledge graph, and results into a single HTTP message. Consequently, MolePro's knowledge graph is accessible to the scientific community through the TRAPI hosted on two servers:
* NCATS Translator server: https://molepro-trapi.transltr.io/molepro/trapi/v1.5/ui/
* Broad Institute server: https://translator.broadinstitute.org/molepro/trapi/v1.5/ui/

# Knowledge Sources
MolePro's knowledge graph is constructed through extensive data scouting and careful data wrangling, integrating information from over two dozen discovered knowledge sources, including:
* _BiGG Models_ http://bigg.ucsd.edu/
* _BigGIM_	http://biggim.ncats.io/api/
* _BindingDB_	https://www.bindingdb.org/
* _ChEBI_	https://www.ebi.ac.uk/chebi
* _ChemBank_	http://chembank.broadinstitute.org/
* _ChEMBL_ https://www.ebi.ac.uk/chembl/
* _CMAP_	https://clue.io/
* _CTD_         http://ctdbase.org/
* _CTRP_	http://portals.broadinstitute.org/ctrp/
* _DepMap_	https://depmap.org/portal/
* _DGIdb_	http://dgidb.org/	
* _DrugBank_	https://www.drugbank.ca/	
* _DrugCentral_	http://drugcentral.org/privacy	
* _Drug Repurposing Hub_	https://clue.io/repurposing
* _DSSTox_      https://www.epa.gov/comptox-tools/distributed-structure-searchable-toxicity-dsstox-database
* _Gelinea_     https://github.com/broadinstitute/GeLiNEA
* _GtoPdb_	https://www.guidetopharmacology.org/
* _HGNC_        https://www.genenames.org	
* _HMDB_	https://www.hmdb.ca/	
* _Inxight:Drugs_	https://drugs.ncats.io/
* _Kinomescan_  https://lincs.hms.harvard.edu/kinomescan/
* _MSigDB_	https://www.gsea-msigdb.org/gsea/msigdb/index.jsp
* _PharmGKB_	https://www.pharmgkb.org/ 
* _Pharos_      https://pharos.nih.gov
* _ProbeMiner_  https://probeminer.icr.ac.uk/#/   
* _PubChem_ https://pubchem.ncbi.nlm.nih.gov/
* _Reactome_    https://reactome.org/
* _RxNorm_	https://www.nlm.nih.gov/research/umls/rxnorm/index.html	
* _SIDER_	http://sideeffects.embl.de/
* _STITCH_	http://stitch.embl.de	
* _STRING_	https://string-db.org/		
	

For additional details about ingested data source see [Catalog of MolePro knowledge sources](https://translator.broadinstitute.org/molecular_data_provider/transformers) (JSON formatted output).

# Source Code

[![MolePro](https://img.shields.io/github/stars/broadinstitute/molecular-data-provider?label=molecular-data-provider&style=social)](https://github.com/broadinstitute/molecular-data-provider)

# External Documentation

[Additional MolePro documentation in GitHub](https://github.com/broadinstitute/molecular-data-provider)
