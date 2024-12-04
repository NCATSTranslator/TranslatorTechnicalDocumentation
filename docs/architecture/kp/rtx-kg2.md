## RTX-KG2 Knowledge Provider Page
[Back to KPs](index.md)

RTX-KG2 is a Translator System Knowledge Provider created/supported/maintained
by
[Team Expander Agent](../../teams/expander-agent.md). It
can answer Translator queries that are expressed in
[TRAPI](https://github.com/NCATSTranslator/ReasonerAPI) format, with query
graphs that contain one node or two nodes connected by an edge (i.e., a
"one-hop" query). RTX-KG2 is backed by the [RTX-KG2 knowledge graph](https://doi.org/10.1186/s12859-022-04932-3), which
integrates dozens of upstream knowledge sources into a Biolink-compliant system, and is 
hosted/served as a TRAPI API using [Plover2.0](https://github.com/RTXteam/PloverDB). For more information about the
RTX-KG2 knowledge graph and how we build it, see the
[RTX-KG2pre build system GitHub project area](https://github.com/RTXteam/RTX-KG2). 
For more information about the
canonicalized version of RTX-KG2 (RTX-KG2c, which underlies the RTX-KG2 API), see [the RTX-KG2c build system project area](https://github.com/RTXteam/RTX/tree/master/code/kg2c).
For more information about the Plover2.0 platform, see the
[PloverDB GitHub project area](https://github.com/RTXteam/PloverDB). 
RTX-KG2 is one of the KPs that is used by the Translator reasoning agent, **ARAX**. For
more information about ARAX, see the
[Expander Agent Page](../../teams/expander-agent.md).

* _Modes of Access_ 

    * Via the Translator API (TRAPI) interface; see [the SmartAPI registry](https://smart-api.info/ui/a6b575139cfd429b0a87f825a625d036)
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
     "https://kg2cploverdb.transltr.io/query" \
     -H  "accept: application/json" \
     -H  "Content-Type: application/json" \
     -d @onehop.json
```
should result in this response:
```
{
  "logs":[
    {
      "level":"INFO",
      "message":"kg2c: Converting qnode n00's 'ids' to equivalent ids we recognize",
      "timestamp":"Fri, 15 Nov 2024 21:11:02 GMT"
    },
    ...
  "message": {
    "knowledge_graph": {
      "edges": {
        "30759528": {
          "attributes":[
            {
              "attribute_source":"infores:rtx-kg2",
              "attribute_type_id":"biolink:knowledge_level",
              "value":"knowledge_assertion"
            },
            {
              "attribute_source":"infores:rtx-kg2",
              "attribute_type_id":"biolink:original_predicate",
              "description":"The IDs of the original RTX-KG2pre edge(s) corresponding to this edge prior to any synonymization or remapping.",
              "value":[
                "CHEMBL.COMPOUND:CHEMBL112---biolink:physically_interacts_with---None---None---None---CHEMBL.TARGET:CHEMBL2094253---identifiers_org_registry:chembl.compound"
              ],
              "value_type_id":"metatype:String"
            },
            {
              "attribute_source":"infores:rtx-kg2",
              "attribute_type_id":"biolink:agent_type",
              "value":"manual_agent"
            }
          ],
          "object":"CHEMBL.TARGET:CHEMBL4523964",
          "predicate":"biolink:physically_interacts_with",
          "sources":[
            {
              "resource_id":"infores:chembl",
              "resource_role":"primary_knowledge_source"
            },
            {
              "resource_id":"infores:rtx-kg2",
              "resource_role":"aggregator_knowledge_source",
              "upstream_resource_ids":[
                "infores:chembl"
              ]
            }
          ],
          "subject":"CHEBI:46195"
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
* SmartAPI registry page for RTX-KG2: https://smart-api.info/ui/a6b575139cfd429b0a87f825a625d036
* Code for the build system for RTX-KG2pre: https://github.com/RTXteam/RTX-KG2
* Code for the build system for RTX-KG2c (canonicalized): https://github.com/RTXteam/RTX/tree/master/code/kg2c
* Code for the Plover2.0 platform used to serve RTX-KG2: https://github.com/RTXteam/PloverDB
