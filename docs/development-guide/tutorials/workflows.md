# Workflows Tutorial

The Operations and Workflow effort aims to define and standardize how Translator components interact and execute tasks. Translator relies on a network of integrated tools and agents, such as ARAs (Autonomous Reasoning Agents), that need to communicate efficiently. However, the operations performed by each component and how these operations are composed into workflows are not always clear or consistent. To address this, the Operations and Workflow work focuses on formally defining operations and workflows, ensuring transparency, configurability, and the ability to interpret results.

The goal is to create standardized operations, build reference implementations, and develop workflows that can be composed and run within the Translator ecosystem. The result is a (continually growing) set of formal definitions, tools, and language that enable developers to discover, interpret, and control Translator operations with greater clarity. 

The [Workflow Runner](https://github.com/NCATSTranslator/workflow-runner) handles the identification of which service can respond to which operation, send to the appropriate endpoints, combine results, and repeat for all operations.

## Summary of operations available

- **lookup**: Searches for relevant entities, such as drugs or diseases, in the knowledge graph based on a query. Options include specifying entity types and sources to query.

- **lookup_and_score**: A combination of looking up entities and scoring the results based on relevance or another criterion. You can customize both the lookup parameters and the scoring method.

- **annotate**: Adds additional information to the knowledge graph, such as annotations to nodes and edges. Options include what type of data to annotate and which parts of the graph to target.

- **annotate_edges**: Annotates the edges in the knowledge graph with attributes that provide more context or meaning. You can specify which edges to annotate and the types of attributes to add.

- **annotate_nodes**: Adds annotations to nodes in the knowledge graph, typically including additional attributes or categories. Options involve selecting nodes and defining the type of annotations.

- **filter_results**: Filters query results based on specific criteria, removing irrelevant results. You can define filtering rules based on attributes or edge properties.

- **filter_results_top_n**: Retains only the top N results in a query based on a chosen attribute or score. You can set N and select the ranking attribute.

- **filter_kgraph**: Filters the knowledge graph by removing irrelevant nodes or edges based on specific criteria. You can set the filtering conditions, such as node or edge properties.

- **filter_kgraph_continuous_kedge_attribute**: Filters edges in the knowledge graph based on continuous attributes, such as numerical values. Options include which attributes to filter and setting thresholds or ranges.

- **filter_kgraph_discrete_kedge_attribute**: A way to filter knowledge graphs (i.e., remove nodes and edges) based on discrete attributes on edges. Options include what attributes, which edges, and whether attached nodes should also be removed.

- **filter_kgraph_discrete_knode_attribute**: Filters nodes based on discrete attributes like categories or types. You can specify the attribute values to use for filtering.

- **filter_kgraph_orphans**: Removes orphan nodes from the knowledge graph (nodes that are not connected to any edges). There are no additional parameters needed beyond identifying orphan nodes.

- **filter_kgraph_percentile**: Filters the graph by selecting nodes or edges that fall within a specific percentile of a given attribute. Options include the percentile thresholds and the attributes to filter by.

- **filter_kgraph_std_dev**: Filters the graph based on standard deviation values of an attribute. You can choose the attributes and set the standard deviation cutoff for filtering.

- **filter_kgraph_top_n**: Filters the knowledge graph to retain only the top N nodes or edges based on a particular attribute. Parameters allow you to specify N and the attribute to use for ranking.

- **overlay**: Adds additional data or overlays relationships onto the existing knowledge graph. Options include specifying which data to overlay and how to integrate it with the existing graph.

- **overlay_compute_jaccard**: Computes the Jaccard similarity between nodes based on shared attributes or connections. You can define which attributes or connections to consider.

- **overlay_compute_ngd**: Computes the Normalized Google Distance (NGD) between nodes to determine their relatedness based on web co-occurrence. This operation does not require additional parameters.

- **overlay_connect_knodes**: Adds new edges between nodes that are found to be related, based on external knowledge or predefined rules. You can specify criteria for creating connections between nodes.

- **overlay_fisher_exact_test**: Performs Fisher's exact test on nodes or edges to determine statistical significance in their relationships. You can choose the attributes or edges to test.

- **bind**: Binds a set of data to specified nodes or edges in the graph. Parameters allow you to choose the nodes or edges to bind the data to.

- **complete_results**: Fills in missing results to ensure the query returns a complete set of data. You can specify the types of results or data sources to complete from.

- **enrich_results**: Enhances the query results by adding related data from external sources or expanding on the existing results. Options include which sources to use and the types of enrichment to apply.

- **fill**: Adds missing nodes or edges to a query graph based on known relationships. You can define which relationships or data sources to use to fill the graph.

- **restate**: Reformulates the query to improve clarity or make it compatible with available data. Options include the specific rules or criteria for restating the query.

- **score**: Assigns scores to query results based on a scoring algorithm, typically to rank the relevance of results. You can configure the scoring algorithm and its parameters.

- **sort_results**: Sorts the query results based on a chosen attribute. You can specify the attribute by which to sort the results.

- **sort_results_edge_attribute**: Sorts query results by the attributes of edges. Options include selecting the edge attribute to use for sorting.

- **sort_results_node_attribute**: Sorts query results by node attributes, such as type or relevance. You can define which node attribute to sort by.

- **sort_results_score**: Sorts query results based on their computed score, ranking them in order of relevance. There are no additional parameters beyond using the score for sorting.

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
