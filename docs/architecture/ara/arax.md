[Back to ARAs](index.md)

## ARAX Autonomous Relay Agent Page

* Accepts queries via [TRAPI](https://ncatstranslator.github.io/TranslatorTechnicalDocumentation/architecture/sri/trapi/) (Translator API) format that triggers automated answering and ranking.
* Accepts queries using ARAXi: a domain-specific language that allows users more fine-grained control on what algorithms are utilized and how when asking their questions.
* Integrated with numerous Knowledge Sources and Knowledge Providers, with automatic (or optionally, manual) specification of what sources and providers are utilized. 

## Technical User Guide to ARAX
There are two main modes for interacting with ARAX: the first is via posting TRAPI messages to the ARAX [API](https://arax.transltr.io/api/arax/v1.4/ui/). Examples of doing this are included [here](https://github.com/RTXteam/RTX/tree/master/code/ARAX/Examples).

The second way to interact with ARAX is via the [GUI](https://arax.transltr.io/). There, you will see four different query types:
1. You can build a query graph by clicking on this icon: ![](https://www.dropbox.com/s/uhe2qtqyzei1aw7/graph.PNG?raw=1)
2. You can paste in a `query_graph` element in a JSON TRAPI message (circumventing the need to manually POST TRAPI queries) by clicking on this icon: ![](https://www.dropbox.com/s/3gw48t4fp5ty33s/JSON.PNG?raw=1)
3. You can enter ARAXi domain specific language commands by clicking on this icon: ![](https://www.dropbox.com/s/khh6whk095vg63c/DSL.PNG?raw=1)
4. You can enter an ARS PK ID (to pull results from the Autonomous Relay System) after clicking on this icon: ![](https://www.dropbox.com/s/ob7ozbxtilpse6o/ID.PNG?raw=1)

No matter which method is used, after submitting a query, the results can be viewed via the links on the left vertical bar under *output*: ![](https://www.dropbox.com/s/1gzovgivoszikym/Output.PNG?raw=1).

If you want to look up an identifier for a specific natural language term, please use the _Synonyms_ link under the *Tools* section of the left vertical bar: ![](https://www.dropbox.com/s/r4a58wg3v3i9imk/Syn.PNG?raw=1)

Each of the query methods has a link to an example so a user can see what sort of information is to be expected. If you run into any issues with using any aspect of the system, please open an issue [here](https://github.com/RTXteam/RTX/issues).

ARAX is registered in Smart API [here](http://smart-api.info/registry?q=arax).

If you would like to deploy your own instance, please see the dependencies listed [here](https://github.com/RTXteam/RTX#installation-and-dependencies), [here](https://github.com/RTXteam/RTX/tree/master/code/reasoningtool/kg-construction#instructions-on-how-to-build-a-new-kg-from-scratch) for how to build the Expander Agent portion of the Knowledge Graph [here](https://github.com/RTXteam/RTX/tree/master/code/reasoningtool/kg-construction#instructions-on-how-to-build-a-new-kg-from-scratch) (more info about this knowledge graph, called KG2, is available [here](../kp/rtx-kg2.md)), and the [deployment wiki](https://github.com/RTXteam/RTX/wiki/Deployment-info). 

## Use Cases 

Please be aware that as BioLink is updated, predicates and categories may change. Similarly, as ARAX deploys new versions, the endpoint may change (eg. `v1.4` in the below), and various other small modifications may be needed in these use-cases.

* one-hop query:

```
cat <<EOF >onehop.json 
{
      "bypass_cache": false,
      "enforce_edge_directionality": false,
      "max_results": 100,
      "message": {
        "query_graph": {
          "edges": {
            "e00": {
              "object": "n01",
              "predicates": ["biolink:interacts_with"],
              "subject": "n00"
            }
          },
          "nodes": {
            "n00": {
              "categories": ["biolink:ChemicalEntity"],
              "ids": ["CHEMBL.COMPOUND:CHEMBL112"]
            },
            "n01": {
              "categories": ["biolink:Protein"]
            }
          }
        }
      },
      "page_number": 1,
      "page_size": 100,
      "return_minimal_metadata": false,
      "stream_progress": false
}
EOF

curl -X POST \
     "https://arax.transltr.io/api/arax/v1.4/query?bypass_cache=false" \
     -H  "accept: application/json" \
     -H  "Content-Type: application/json" \
     -d @onehop.json
```
should result in something similar to this response:
```
{
  "context": "https://raw.githubusercontent.com/biolink/biolink-model/master/context.jsonld",
  "datetime": "2021-05-10 11:56:19",
  "description": "Normal completion",
  "id": "https://arax.transltr.io/api/arax/v1.4/response/9182",
  "logs": [
    {
      "code": "",
      "level": "INFO",
      "message": "ARAX Query launching on incoming Query",
      "timestamp": "2021-05-10T11:56:19.774118"
    },
    ...
  ],
  "message": {
    "knowledge_graph": {
      "edges": {
        "ARAX/KG2:CHEBI:4056-biolink:physically_interacts_with-CHEMBL.COMPOUND:CHEMBL112": {
          "attributes": [
            {
              "attribute_source": "infores:rtx_kg2_kp",
              "attribute_type_id": "biolink:original_source",
              "value": "infores:semmeddb",
              "value_type_id": "biolink:InformationResource"
            },
            {
              "attribute_source": "infores:semmeddb",
              "attribute_type_id": "biolink:has_supporting_publications",
              "value": [
                "PMID:10872641",
                "PMID:11330834",
                "PMID:23032911",
                "PMID:25319358",
                "PMID:25753323",
                "PMID:25956474",
                "PMID:30293568",
                "PMID:30915487",
                "PMID:31600996"
              ],
              "value_type_id": "biolink:Publication"
            },
            {
              "attribute_source": "infores:arax_ara",
              "attribute_type_id": "biolink:knowledge_provider_source",
              "value": "infores:rtx_kg2_kp",
              "value_type_id": "biolink:InformationResource"
            }
          ],
          "object": "CHEMBL.COMPOUND:CHEMBL112",
          "predicate": "biolink:physically_interacts_with",
          "subject": "CHEBI:4056"
        },
        "ARAX/KG2:CHEMBL.COMPOUND:CHEMBL112-biolink:molecularly_interacts_with-UniProtKB:O00519": {
          "attributes": [
            {
              "attribute_source": "infores:rtx_kg2_kp",
              "attribute_type_id": "biolink:original_source",
              "value": "infores:chembl",
              "value_type_id": "biolink:InformationResource"
            },
            {
              "attribute_source": "infores:arax_ara",
              "attribute_type_id": "biolink:knowledge_provider_source",
              "value": "infores:rtx_kg2_kp",
              "value_type_id": "biolink:InformationResource"
            }
          ],
          "object": "UniProtKB:O00519",
          "predicate": "biolink:molecularly_interacts_with",
          "subject": "CHEMBL.COMPOUND:CHEMBL112"
        },
        "ARAX/KG2:CHEMBL.COMPOUND:CHEMBL112-biolink:molecularly_interacts_with-UniProtKB:P08684": {
          "attributes": [
            {
              "attribute_source": "infores:rtx_kg2_kp",
              "attribute_type_id": "biolink:original_source",
              "value": "infores:pharos",
              "value_type_id": "biolink:InformationResource"
            },
            {
              "attribute_source": "infores:arax_ara",
              "attribute_type_id": "biolink:knowledge_provider_source",
              "value": "infores:rtx_kg2_kp",
              "value_type_id": "biolink:InformationResource"
            }
          ],
          "object": "UniProtKB:P08684",
          "predicate": "biolink:molecularly_interacts_with",
          "subject": "CHEMBL.COMPOUND:CHEMBL112"
        },
        "ARAX/KG2:CHEMBL.COMPOUND:CHEMBL112-biolink:molecularly_interacts_with-UniProtKB:P10635": {
          "attributes": [
            {
              "attribute_source": "infores:rtx_kg2_kp",
              "attribute_type_id": "biolink:original_source",
              "value": "infores:pharos",
              "value_type_id": "biolink:InformationResource"
            },
            {
              "attribute_source": "infores:arax_ara",
              "attribute_type_id": "biolink:knowledge_provider_source",
              "value": "infores:rtx_kg2_kp",
              "value_type_id": "biolink:InformationResource"
            }
          ],
          "object": "UniProtKB:P10635",
          "predicate": "biolink:molecularly_interacts_with",
          "subject": "CHEMBL.COMPOUND:CHEMBL112"
        },
        "ARAX/KG2:CHEMBL.COMPOUND:CHEMBL112-biolink:molecularly_interacts_with-UniProtKB:P12268": {
          "attributes": [
            {
              "attribute_source": "infores:rtx_kg2_kp",
              "attribute_type_id": "biolink:original_source",
              "value": "infores:pharos",
              "value_type_id": "biolink:InformationResource"
            },
            {
              "attribute_source": "infores:arax_ara",
              "attribute_type_id": "biolink:knowledge_provider_source",
              "value": "infores:rtx_kg2_kp",
              "value_type_id": "biolink:InformationResource"
            }
          ],
          "object": "UniProtKB:P12268",
          "predicate": "biolink:molecularly_interacts_with",
          "subject": "CHEMBL.COMPOUND:CHEMBL112"
        },
        ...   
```
* two-hop query with several various overlay commands and filtering:

```
cat <<EOF >kitchensink.json 
{
  "bypass_cache": false,
  "enforce_edge_directionality": false,
  "max_results": 100,
  "message": {},
    "operations": {"actions": [
            "add_qnode(name=arthritis, key=n00)",
            "add_qnode(categories=biolink:Protein, is_set=true, key=n01)",
            "add_qnode(categories=biolink:ChemicalSubstance, key=n02)",
            "add_qedge(subject=n00, object=n01, key=e00)",
            "add_qedge(subject=n01, object=n02, key=e01, predicates=biolink:physically_interacts_with)",
            "expand(edge_key=[e00,e01], kp=ARAX/KG2)",
            "overlay(action=overlay_clinical_info, observed_expected_ratio=true, virtual_relation_label=C1, subject_qnode_key=n00, object_qnode_key=n02)",
            "filter_kg(action=remove_edges_by_attribute, edge_attribute=probably_treats, direction=below, threshold=.8, remove_connected_nodes=t, qnode_key=n02)",
            "overlay(action=compute_jaccard, start_node_key=n00, intermediate_node_key=n01, end_node_key=n02, virtual_relation_label=J1)",
            "overlay(action=predict_drug_treats_disease, subject_qnode_key=n02, object_qnode_key=n00, virtual_relation_label=P1)",
            "resultify(ignore_edge_direction=true)",
            "filter_results(action=limit_number_of_results, max_results=15)",
            "return(message=true, store=false)"
        ]},
  "page_number": 1,
  "page_size": 100,
  "return_minimal_metadata": false,
  "stream_progress": false
}
EOF

curl -X POST \
     "https://https://arax.transltr.io/api/arax/v1.4/query?bypass_cache=false" \
     -H  "accept: application/json" \
     -H  "Content-Type: application/json" \
     -d @kitchensink.json
```
should result in this response: (This utilizes a few different overlay commands which hit a few databases so this may take a minute or two)
```
{
  "context": "https://raw.githubusercontent.com/biolink/biolink-model/master/context.jsonld",
  "datetime": "2021-05-10 11:36:58",
  "description": "Normal completion",
  "logs": [
    ...
  ],
  "message": {
    "knowledge_graph": {
      "edges": {
        "ARAX/KG2:CHEBI:67079-biolink:physically_interacts_with-CHEMBL.TARGET:CHEMBL1641359": {
          "attributes": [
            {
              "attribute_source": "infores:rtx_kg2_kp",
              "attribute_type_id": "biolink:original_source",
              "value": "infores:semmeddb",
              "value_type_id": "biolink:InformationResource"
            },
            {
              "attribute_source": "infores:semmeddb",
              "attribute_type_id": "biolink:has_supporting_publications",
              "value": [
                "PMID:22552402",
                "PMID:27320659",
                "PMID:30199704"
              ],
              "value_type_id": "biolink:Publication"
            },
            {
              "attribute_source": "infores:arax_ara",
              "attribute_type_id": "biolink:knowledge_provider_source",
              "value": "infores:rtx_kg2_kp",
              "value_type_id": "biolink:InformationResource"
            }
          ],
          "object": "CHEMBL.TARGET:CHEMBL1641359",
          "predicate": "biolink:physically_interacts_with",
          "subject": "CHEBI:67079"
        },
        "ARAX/KG2:CHEBI:67079-biolink:physically_interacts_with-CHEMBL.TARGET:CHEMBL3301559": {
          "attributes": [
            {
              "attribute_source": "infores:rtx_kg2_kp",
              "attribute_type_id": "biolink:original_source",
              "value": "infores:semmeddb",
              "value_type_id": "biolink:InformationResource"
            },
            {
              "attribute_source": "infores:semmeddb",
              "attribute_type_id": "biolink:has_supporting_publications",
              "value": [
                "PMID:29427163"
              ],
              "value_type_id": "biolink:Publication"
            },
            {
              "attribute_source": "infores:arax_ara",
              "attribute_type_id": "biolink:knowledge_provider_source",
              "value": "infores:rtx_kg2_kp",
              "value_type_id": "biolink:InformationResource"
            }
          ],
          "object": "CHEMBL.TARGET:CHEMBL3301559",
          "predicate": "biolink:physically_interacts_with",
          "subject": "CHEBI:67079"
        },
        "ARAX/KG2:CHEBI:67079-biolink:physically_interacts_with-UniProtKB:O00206": {
          "attributes": [
            {
              "attribute_source": "infores:rtx_kg2_kp",
              "attribute_type_id": "biolink:original_source",
              "value": "infores:semmeddb",
              "value_type_id": "biolink:InformationResource"
            },
            {
              "attribute_source": "infores:semmeddb",
              "attribute_type_id": "biolink:has_supporting_publications",
              "value": [
                "PMID:30099678"
              ],
              "value_type_id": "biolink:Publication"
            },
            {
              "attribute_source": "infores:arax_ara",
              "attribute_type_id": "biolink:knowledge_provider_source",
              "value": "infores:rtx_kg2_kp",
              "value_type_id": "biolink:InformationResource"
            }
          ],
          "object": "UniProtKB:O00206",
          "predicate": "biolink:physically_interacts_with",
          "subject": "CHEBI:67079"
        },
        "ARAX/KG2:CHEBI:67079-biolink:physically_interacts_with-UniProtKB:P01137": {
          "attributes": [
            {
              "attribute_source": "infores:rtx_kg2_kp",
              "attribute_type_id": "biolink:original_source",
              "value": "infores:semmeddb",
              "value_type_id": "biolink:InformationResource"
            },
            {
              "attribute_source": "infores:semmeddb",
              "attribute_type_id": "biolink:has_supporting_publications",
              "value": [
                "PMID:15285804"
              ],
              "value_type_id": "biolink:Publication"
            },
            {
              "attribute_source": "infores:arax_ara",
              "attribute_type_id": "biolink:knowledge_provider_source",
              "value": "infores:rtx_kg2_kp",
              "value_type_id": "biolink:InformationResource"
            }
          ],
          "object": "UniProtKB:P01137",
          "predicate": "biolink:physically_interacts_with",
          "subject": "CHEBI:67079"
        },
...
```


## Knowledge Providers Accessed
Currently, ARAX will query every SmartAPI registered, TRAPI compliant KP. These include:

* [Clinical Data Provider](https://github.com/NCATSTranslator/NCATSTranslator.github.io/wiki/Clinical-Data-Provider)
* [Exposure Provider](https://github.com/NCATSTranslator/NCATSTranslator.github.io/wiki/Exposure-Provider)
* [Molecular Data Provider](https://github.com/NCATSTranslator/NCATSTranslator.github.io/wiki/Molecular-Data-Provider)
* [Service Provider](https://github.com/NCATSTranslator/NCATSTranslator.github.io/wiki/Service-Provider)
* [Genetics Provider](https://github.com/NCATSTranslator/Translator-All/wiki/Genetics-Knowledge-Provider)
* [Connections Hypothesis Provider](https://github.com/NCATSTranslator/Translator-All/wiki/Connections-Hypothesis-Provider)
* [RTX-KG2](https://smart-api.info/registry?q=00bab7d59abe031098d5cb1597f7f1c4)

## Source Code
* The entire codebase is accessible at [https://github.com/RTXteam/RTX/](https://github.com/RTXteam/RTX/)

## External Documentation
* ARAXi Domain Specific Language documentation: [https://github.com/RTXteam/RTX/blob/master/code/ARAX/Documentation/DSL_Documentation.md](https://github.com/RTXteam/RTX/blob/master/code/ARAX/Documentation/DSL_Documentation.md)
* Project README: [https://github.com/RTXteam/RTX/blob/master/README.md](https://github.com/RTXteam/RTX/blob/master/README.md)
