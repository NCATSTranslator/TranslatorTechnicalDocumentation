## RTX-KG2 Knowledge Provider Page
[Back to Home](..)

RTX-KG2 is a Translator System Knowledge Provider created/supported/maintained
by
[Team Expander Agent](../../../teams/expander-agent). It
can answer Translator queries that are expressed in
[TRAPI](https://github.com/NCATSTranslator/ReasonerAPI) format, with query
graphs that contain one node or two nodes connected by an edge (i.e., a
"one-hop" query). RTX-KG2 is backed by the RTX-KG2 knowledge graph, which
integrates dozens of upstream knowledge sources into a Biolink-compliant system
hosted in a custom in-memory database (PloverDB). For more information about the
RTX-KG2 knowledge graph and how we built it, see the
[RTX-KG2 build system GitHub project area](https://github.com/RTXteam/RTX-KG2). For
more information about the PloverDB database, see the
[PloverDB GitHub project area](https://github.com/RTXteam/PloverDB). RTX-KG2 is
one of the KPs that is used by the Translator reasoning agent, **ARAX**. For
more information about ARAX, see the
[Expander Agent Page](../../../teams/expander-agent).

* _Modes of Access_ 

    * Via the Translator API (TRAPI) interface; see [the SmartAPI registry](https://smart-api.info/ui/00bab7d59abe031098d5cb1597f7f1c4)
    * Download RTX-KG2 knowledge graph in [KGX TSV](https://github.com/biolink/kgx/blob/master/specification/kgx-format.md) format from the [NCATS GitHub git-lfs repository](https://github.com/ncats/translator-lfs-artifacts/tree/main/files).
    * Build your own RTX-KG2: [instructions here](https://github.com/RTXteam/RTX-KG2#how-to-build-rtx-kg2-from-its-upstream-sources)

* Issues using the RTX-KG2 KP should be logged in the [RTX-KG2 issue tracker](https://github.com/RTXteam/RTX-KG2/issues).

* _How to build your own instance for NCATS Deployment pipeline_


**Use Cases**- 

* one-hop query:

```
cat <<EOF >onehop.json 
{
  "message":{
    "query_graph":{
      "nodes":{
        "n00":{
          "ids":["CHEMBL.COMPOUND:CHEMBL112"],
          "categories":[
            "biolink:Drug"
          ],
          "is_set":false
        },
        "n01":{
          "categories":[
            "biolink:Gene",
            "biolink:Protein"
          ],
          "is_set":false
        }
      },
      "edges":{
        "e00":{
          "predicates":[
            "biolink:interacts_with"
          ],
          "subject":"n00",
          "object":"n01",
          "exclude":false
        }
      }
    }
  }
}
EOF

curl -X POST \
     "https://arax.ncats.io/api/rtxkg2/v1.3/query?bypass_cache=false" \
     -H  "accept: application/json" \
     -H  "Content-Type: application/json" \
     -d @onehop.json
```
should result in this response:
```
{
  "context": "https://raw.githubusercontent.com/biolink/biolink-model/master/context.jsonld",
  "datetime": "2021-04-28 04:54:14",
  "description": "Normal completion",
  "logs": [
    {
      "code": "",
      "level": "INFO",
      "message": "RTXKG2 Query launching on incoming Query",
      "timestamp": "2021-04-28T04:54:14.856515"
    },
    ...
  ],
  "message": {
    "knowledge_graph": {
      "edges": {
        "1447028": {
          "attributes": [
            {
              "name": "provided_by",
              "type": "biolink:provided_by",
              "value": [
                "identifiers_org_registry:chembl.compound"
              ]
            }
          ],
          "object": "UniProtKB:O00519",
          "predicate": "biolink:molecularly_interacts_with",
          "subject": "CHEMBL.COMPOUND:CHEMBL112"
        },
        "1447029": {
          "attributes": [
            {
              "name": "provided_by",
              "type": "biolink:provided_by",
              "value": [
                "identifiers_org_registry:chembl.compound"
              ]
            }
          ],
          "object": "UniProtKB:O14965",
          "predicate": "biolink:molecularly_interacts_with",
          "subject": "CHEMBL.COMPOUND:CHEMBL112"
        },
        "1447030": {
          "attributes": [
            {
              "name": "provided_by",
              "type": "biolink:provided_by",
              "value": [
                "identifiers_org_registry:chembl.compound"
              ]
            }
          ],
          "object": "UniProtKB:O43570",
          "predicate": "biolink:molecularly_interacts_with",
          "subject": "CHEMBL.COMPOUND:CHEMBL112"
        },
        "1447031": {
          "attributes": [
            {
              "name": "provided_by",
              "type": "biolink:provided_by",
              "value": [
                "pharos:"
              ]
            }
          ],
          "object": "UniProtKB:P00797",
          "predicate": "biolink:molecularly_interacts_with",
          "subject": "CHEMBL.COMPOUND:CHEMBL112"
        },
        "1447032": {
          "attributes": [
            {
              "name": "provided_by",
              "type": "biolink:provided_by",
              "value": [
                "identifiers_org_registry:chembl.compound"
              ]
            }
          ],
          "object": "UniProtKB:P00915",
          "predicate": "biolink:molecularly_interacts_with",
          "subject": "CHEMBL.COMPOUND:CHEMBL112"
        },
        "1447033": {
          "attributes": [
            {
              "name": "provided_by",
              "type": "biolink:provided_by",
              "value": [
                "identifiers_org_registry:chembl.compound"
              ]
            }
          ],
          "object": "UniProtKB:P06746",
          "predicate": "biolink:molecularly_interacts_with",
          "subject": "CHEMBL.COMPOUND:CHEMBL112"
        },
        "1447034": {
          "attributes": [
            {
              "name": "provided_by",
              "type": "biolink:provided_by",
              "value": [
                "identifiers_org_registry:chembl.compound"
              ]
            }
          ],
          "object": "UniProtKB:P07550",
          "predicate": "biolink:molecularly_interacts_with",
          "subject": "CHEMBL.COMPOUND:CHEMBL112"
        },
        ...   
```

**Knowledge Sources Accessed** - See the [FAQ entry "What data sources are used in KG2?"](https://github.com/RTXteam/RTX/tree/master/code/kg2#what-data-sources-are-used-in-kg2) for details.
* [Biolink model](https://biolink.github.io/biolink-model/)
* [ChEMBL](https://www.ebi.ac.uk/chembl/)
* [DGIdb](https://www.dgidb.org/)
* [DisGeNET](https://www.disgenet.org/)
* [DrugBank](https://go.drugbank.com)
* [DrugCentral](https://drugcentral.org/)
* [EFO](https://www.ebi.ac.uk/efo/)
* [Ensembl](https://ensembl.org)  (Ensembl Genes, for human)
* [Gene Ontology annotations](https://www.ebi.ac.uk/GOA/index) (from EBI)
* [HMDB](https://hmdb.ca)
* [IntAct](https://www.ebi.ac.uk/intact/)
* [Jensen Lab Diseases](https://diseases.jensenlab.org/)
* [KEGG](https://www.genome.jp/kegg/) (via API)
* [miRBase](https://mirbase.org)
* [NCBI Gene](https://www.ncbi.nlm.nih.gov/gene)
* [OBO Foundry ontologies](http://www.obofoundry.org/) 
  * BFO
  * CHEBI
  * GO-plus
  * RO
  * UBERON
  * FMA
  * DDANAT
  * CL
  * FOODON
  * EHDAA2
  * BSPO
  * HP
  * NBO
  * NCBI taxslim
  * PATO
  * MONDO
  * DOID
  * PR
  * INO
  * GENEPIO
  * MI
* [PathWhiz](https://smpdb.ca/pathwhiz)
* [Reactome](https://reactome.org)
* [repoDB](https://portal.dbmi.hms.harvard.edu/projects/repoDB/)
* [SemMedDB](https://skr3.nlm.nih.gov/SemMedDB/)
* [SMPDB](https://smpdb.ca)
* [TTD](http://db.idrblab.net/ttd/)
* [UMLS](https://www.nlm.nih.gov/research/umls/index.html) 
  * UMLS Semantic Types
  * ATC
  * CPT
  * DRUGBANK
  * FMA
  * GO
  * HCPCS
  * HCPT
  * HGNC
  * HL7
  * HPO
  * ICD10
  * ICD10AE
  * ICD10CM
  * ICD10PCS
  * ICD9CM
  * LNC
  * MDR
  * MED-RT
  * MEDLINEPLUS
  * MESH
  * NCBI
  * NCI
  * NDDF
  * NDFRT
  * OMIM
  * PDQ
  * PSY
  * RXNORM
  * SNOMEDCT
  * VANDF
* [UniChem](https://www.ebi.ac.uk/unichem/) (cross-references between Chebi, ChEMBL compound, DrugBank, HMDB, KEGG, and DrugCentral identifiers)
* [UniProtKB](https://www.uniprot.org/help/uniprotkb)

**Source Code** - (include links to your source code). See example below
* Example [python module](https://github.com/RTXteam/RTX/blob/master/code/ARAX/Examples/kg2_api_example.py) that queries the KG2 KP API

**External Documentation** (List of urls for documentation sites). See example below. 
* SmartAPI registry page for RTX-KG2: https://smart-api.info/ui/00bab7d59abe031098d5cb1597f7f1c4
* Code for the build system for RTX-KG2: https://github.com/RTXteam/RTX/tree/master/code/kg2
* Code for PloverDB database used by RTX-KG2 service: https://github.com/RTXteam/PloverDB
