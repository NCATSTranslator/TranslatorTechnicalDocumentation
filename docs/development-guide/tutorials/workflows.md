# Workflows Tutorial

The Operations and Workflow effort aims to define and standardize how Translator components interact and execute tasks. Translator relies on a network of integrated tools and agents, such as ARAs (Autonomous Reasoning Agents), that need to communicate efficiently. However, the operations performed by each component and how these operations are composed into workflows are not always clear or consistent. To address this, the Operations and Workflow work focuses on formally defining operations and workflows, ensuring transparency, configurability, and the ability to interpret results.

The goal is to create standardized operations, build reference implementations, and develop workflows that can be composed and run within the Translator ecosystem. The result is a (continually growing) set of formal definitions, tools, and language that enable developers to discover, interpret, and control Translator operations with greater clarity. 

## Simple example

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
