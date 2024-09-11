# Workflows Tutorial

The Operations and Workflow effort aims to define and standardize how Translator components interact and execute tasks. Translator relies on a network of integrated tools and agents, such as ARAs (Autonomous Reasoning Agents), that need to communicate efficiently. However, the operations performed by each component and how these operations are composed into workflows are not always clear or consistent. To address this, the Operations and Workflow work focuses on formally defining operations and workflows, ensuring transparency, configurability, and the ability to interpret results.

The goal is to create standardized operations, build reference implementations, and develop workflows that can be composed and run within the Translator ecosystem. The result is a (continually growing) set of formal definitions, tools, and language that enable developers to discover, interpret, and control Translator operations with greater clarity. 

The [Workflow Runner](https://github.com/NCATSTranslator/workflow-runner) handles the identification of which service can respond to which operation, send to the appropriate endpoints, combine responses, and repeat for all operations. Some ARAs can also handle Workflow operations. Please see [here](../../architecture/workflows.md) for more information about the workflow runner.

The [Curated Query Service (CQS)](https://github.com/TranslatorSRI/CQS/tree/main) is an example of a service that leverages the Operations & Workflows. 

## Summary of operations available

- **lookup**: This operation adds knodes/kedges, (complete) results, and scores (to the results). It is equivalent to the workflow fill + bind + complete_results + score. Any constraints attached to QNodes and QEdges specified in the TRAPI must be respected.

- **lookup_and_score**: This operation adds knodes/kedges, (complete) results, and scores (to the results). It is equivalent to the workflow fill + bind + complete_results + score. Any constraints attached to QNodes and QEdges specified in the TRAPI must be respected.

- **annotate**: This operation adds attributes to knowledge graph elements.

- **annotate_edges**: This operation adds attributes to knowledge graph edges.

- **annotate_nodes**: This operation adds attributes to knowledge graph nodes.

- **bind**: This operation adds results binding kgraph elements to qgraph elements.

- **complete_results**: This operation combines partial results into complete results.

- **enrich_results**: Create new results by applying enrichment analysis to existing results. In particular, combines results by transforming a qnode into a set, formed of knodes that share a property or relation more often than expected by chance.

- **fill**: This operation adds knodes and kedges. Any constraints attached to QNodes and QEdges specified in the TRAPI must be respected.

- **filter_kgraph**: This operation removes kgraph elements (nodes and/or edges).

- **filter_kgraph_continuous_kedge_attribute**: This operation removes kgraph edges based on the value of a continuous edge attribute. Edges without the given attribute are left alone.

- **filter_kgraph_discrete_kedge_attribute**: This operation removes kgraph edges which have a discrete attribute containing the specified value. Edges without the given attribute are left alone.

- **filter_kgraph_discrete_knode_attribute**: This operation removes kgraph nodes which have a discrete attribute containing the specified value. Edges connecting to the removed nodes will also be removed.

- **filter_kgraph_orphans**: This operation removes kgraph elements that are not referenced by any results.

- **filter_kgraph_percentile**: This operation removes kgraph edges that have attribute values below/above the given percentile.

- **filter_kgraph_std_dev**: This operation removes kgraph edges that have attribute values below/above the mean +/- n standard deviations.

- **filter_kgraph_top_n**: This operation removes all but the top N knowledge graph edges based on a specified edge attribute.

- **filter_results**: This operation removes query results.

- **filter_results_top_n**: This operation removes all but the top N results based on a result attribute.

- **overlay**: This operation adds edges to the knowledge graph that did not exist before by leveraging new relationships or data.

- **overlay_compute_jaccard**: This operation computes the Jaccard similarity coefficient between nodes, adding the result as an edge attribute in the knowledge graph.

- **overlay_compute_ngd**: This operation adds NGD (Normalized Google Distance) values as edge attributes in the knowledge graph for pairs of nodes.

- **overlay_connect_knodes**: This operation adds edges connecting knodes that were not previously connected in the kgraph, adding all possible kedges containing node bindings to both the subject and object knodes.

- **overlay_fisher_exact_test**: This operation computes Fisher's Exact Test p-values for connections between nodes and adds this information as an edge attribute to the knowledge graph.

- **restate**: This operation modifies the query graph.

- **score**: This operation adds scores to results.

- **sort_results**: This operation allows the TRAPI server to sort the elements of the list of results.

- **sort_results_edge_attribute**: This operation sorts the results by a given edge attribute.

- **sort_results_node_attribute**: This operation sorts the results by a given node attribute.

- **sort_results_score**: This operation sorts the results by the result score.


## Simple example of a workflow query

Here's a simple example for running an operation and workflow query for finding drugs that treat neutropenia. We will walk through the steps involved in defining a workflow, creating a query graph, and submitting it to the ARAX endpoint using cURL.

### Step 1: Create Your Workflow

In this step, we define the operations that will be performed by the workflow. For this example, we will use two operations:
1. `lookup`: This operation finds knowledge related to the given nodes and edges in the query.
2. `score`: This operation assigns scores to the results based on certain criteria.

Here’s a JSON definition for the workflow that looks up drugs treating neutropenia and then scores them. Note the `workflow` field.

```json
{
  "workflow": [
    {
      "id": "lookup"
    },
    {
      "id": "score"
    }
  ],
  "message": {
    "query_graph": {
      "edges": {
        "e0": {
          "subject": "n1",
          "object": "n0",
          "predicates": [
            "biolink:treats_or_applied_or_studied_to_treat"
          ]
        }
      },
      "nodes": {
        "n0": {
          "ids": [
            "MONDO:0001475"
          ],
          "is_set": false,
          "categories": [
            "biolink:Disease"
          ],
          "name": "MONDO:0001475"
        },
        "n1": {
          "is_set": false,
          "categories": [
            "biolink:Drug"
          ]
        }
      }
    }
  },
  "submitter": "ARAX GUI",
  "stream_progress": true,
  "query_options": {
    "kp_timeout": "30",
    "prune_threshold": "50"
  }
}
```

#### Explanation:
- **`workflow`**: This contains the steps to perform in sequence (`lookup` and `score`).
- **`message`**: This is the TRAPI query graph query we’re sending to the Translator. It includes:
  - A query graph with nodes (n0: neutropenia disease and n1: drugs) and an edge (e0) connecting them, with the `biolink:treats_or_applied_or_studied_to_treat` predicate.
  - **`n0`** is the disease node representing neutropenia with the identifier `MONDO:0001475`.
  - **`n1`** is a drug node, representing drugs in general.
  
### Step 2: Save the Workflow as a JSON File

Save the JSON workflow in a file called `workflow.json`.

### Step 3: Submit the Query Using cURL

Once the workflow is saved, use the following cURL command to send the request to the ARAX Translator API:

```bash
curl -X POST \
     "https://arax.ncats.io/api/arax/v1.4/query?bypass_cache=false" \
     -H  "accept: application/json" \
     -H  "Content-Type: application/json" \
     -d @workflow.json
```

This command sends the `workflow.json` file to the ARAX API and returns a JSON response containing the results.

### Step 4: View the Results

The response will contain various details, such as a list of drugs that treat neutropenia, along with scores and publications supporting the associations.

The structure of the response will look something like this:

```json
{
  "biolink_version": "4.2.0",
  "context": "https://raw.githubusercontent.com/biolink/biolink-model/master/context.jsonld",
  "datetime": "2024-09-10 18:35:13",
  "description": "Normal completion",
  "id": "https://arax.ncats.io/api/arax/v1.4/response/293677",
  "info": null,
  "job_id": null,
  "logs": <snip>
"message": {
    "auxiliary_graphs": null,
    "knowledge_graph": {
      "edges": {
        "infores:rtx-kg2:CHEBI:10023--biolink:treats_or_applied_or_studied_to_treat--None--None--None--MONDO:0001475--infores:semmeddb": {
          "attributes": [
            {
              "attribute_source": "infores:semmeddb",
              "attribute_type_id": "biolink:publications",
              "attributes": null,
              "description": null,
              "original_attribute_name": null,
              "value": [
                "PMID:12746374",
                "PMID:14638514",
                "PMID:15472346",
                "PMID:16121307",
                "PMID:16838224",
                "PMID:18154475",
                "PMID:21482497",
                "PMID:22712456",
                "PMID:26351595",
                "PMID:28630185",
                "PMID:29194488"
              ],
              "value_type_id": "biolink:Uriorcurie",
              "value_url": null
            },
            {
              "attribute_source": "infores:semmeddb",
              "attribute_type_id": "bts:sentence",
              "attributes": null,
              "description": null,
              "original_attribute_name": null,
              "value": {
                "PMID:12746374": {
                  "object score": "928",
                  "publication date": "2003 Jun",
                  "sentence": "Outbred ICR mice were rendered neutropenic, infected intravenously with Fusarium solani and treated orally with voriconazole.",
                  "subject score": "1000"
                },
                "PMID:14638514": {
                  "object score": "853",
                  "publication date": "2003 Dec",
                  "sentence": "Efficacy of voriconazole in treatment of systemic scedosporiosis in neutropenic mice.",
                  "subject score": "1000"
                },
                "PMID:15472346": {
                  "object score": "853",
                  "publication date": "2004 Oct",
                  "sentence": "In summary, this report describes the successful treatment of invasive pulmonary A. ustus infection by lung resection and antifungal treatment with voriconazole in a neutropenic patient.",
                  "subject score": "1000"
                },
                "PMID:16121307": {
                  "object score": "853",
                  "publication date": "1999 Sep",
                  "sentence": "Voriconazole is effective and well-tolerated in the treatment of neutropenic patients with acute invasive aspergillosis [187877], non-neutropenic patients with chronic invasive aspergillosis [187878] and HIV patients with oropharyngeal candidiasis [187866].",
                  "subject score": "1000"
                },
                "PMID:16838224": {
                  "object score": "853",
                  "publication date": "2006 Aug 15",
                  "sentence": "This case report illustrates that voriconazole may be useful in the treatment of disseminated T. asahii infection in neutropenic patients.",
                  "subject score": "1000"
                },
                "PMID:18154475": {
                  "object score": "1000",
                  "publication date": "2008 Jan",
                  "sentence": "CONCLUSION: Oral voriconazole appears to be a safe empiric antifungal treatment with an encouraging rate of activity for patients with neutropenia and uncomplicated persistent fever.",
                  "subject score": "888"
                },
                "PMID:21482497": {
                  "object score": "1000",
                  "publication date": "2011 Feb",
                  "sentence": "Oral voriconazole for neutropenia: a leukemia patient with probable pulmonary aspergillosis and scedosporidiosis.",
                  "subject score": "888"
                },
                "PMID:22712456": {
                  "object score": "1000",
                  "publication date": "2013 Apr",
                  "sentence": "Neutropenia (OR 0.1, P= 0.008) and immunosuppression (OR 0.1, P= 0.004) were independently associated with 2-week successful response after voriconazole therapy.",
                  "subject score": "888"
                },
                "PMID:26351595": {
                  "object score": "853",
                  "publication date": "2015",
                  "sentence": "There is no conclusive evidence that the antifungal agent voriconazole is effective in the neutropenic patients infected with Trichosporon asahii.",
                  "subject score": "901"
                },
                "PMID:28630185": {
                  "object score": "789",
                  "publication date": "2017 09",
                  "sentence": "PC945, posaconazole, or voriconazole was administered intranasally once daily on days 0 to 3 (early intervention) or days 1 to 3 (late intervention) postinfection in temporarily neutropenic A/J mice infected intranasally with A. fumigatus, and bronchoalveolar lavage fluid (BALF) and serum were collected on day 3.",
                  "subject score": "1000"
                },
                "PMID:29194488": {
                  "object score": "853",
                  "publication date": "2017 Nov 29",
                  "sentence": "Conclusions: Isavuconazole had comparable efficacy and safety to voriconazole in neutropenic patients with IA.",
                  "subject score": "1000"
                }
              },
              "value_type_id": null,
              "value_url": null
            ,
<snip>
  "resource_id": "ARAX",
  "restated_question": null,
  "schema_version": "1.5.0",
  "status": "Success",
  "submitter": "ARAX GUI",
  "table_column_names": [
    "score",
    "essence",
    "essence_category"
  ],
  "tool_version": "ARAX 1.5.3",
  "total_results_count": 51,
  "type": "translator_reasoner_response",
  "validation_result": null,
  "workflow": null
}
```

In the `knowledge_graph` section, you will see edges connecting drugs (e.g., CHEBI:10023) to the disease `MONDO:0001475`, along with supporting evidence from literature (e.g., PubMed IDs).

### Step 5: Explore and Interpret Results

The API response will also include details like the score of each drug-disease relationship, specific sentences from publications, and more. You can use this information to interpret which drugs are most relevant to neutropenia based on the scoring.

## A more complicated example

Here is an example that specifies a certain KP to call, overlays with additional information (Fisher Exact Test and Normalized Google Distance), scores it, and limits the number of results.

```
{
  "workflow": [
    {
      "id": "fill",
      "parameters": {
        "allowlist": [
          "infores:rtx-kg2"
        ],
        "qedge_keys": [
          "e0"
        ]
      }
    },
    {
      "id": "bind"
    },
    {
      "id": "overlay_compute_ngd",
      "parameters": {
        "virtual_relation_label": "NGD1",
        "qnode_keys": [
          "n0",
          "n1"
        ]
      }
    },
    {
      "id": "overlay_fisher_exact_test",
      "parameters": {
        "subject_qnode_key": "n0",
        "object_qnode_key": "n1",
        "virtual_relation_label": "FET1"
      }
    },
    {
      "id": "complete_results"
    },
    {
      "id": "score"
    },
    {
      "id": "filter_results_top_n",
      "parameters": {
        "max_results": 10
      }
    }
  ],
  "message": {
    "query_graph": {
      "edges": {
        "e0": {
          "subject": "n1",
          "object": "n0",
          "predicates": [
            "biolink:treats_or_applied_or_studied_to_treat"
          ]
        }
      },
      "nodes": {
        "n0": {
          "ids": [
            "MONDO:0001475"
          ],
          "is_set": false,
          "categories": [
            "biolink:Disease"
          ],
          "name": "MONDO:0001475"
        },
        "n1": {
          "is_set": false,
          "categories": [
            "biolink:Drug"
          ]
        }
      }
    }
  },
  "submitter": "ARAX GUI",
  "stream_progress": true,
  "query_options": {
    "kp_timeout": "30",
    "prune_threshold": "50"
  }
}
```
You can see the overlain information in the result analysis support graphs.
