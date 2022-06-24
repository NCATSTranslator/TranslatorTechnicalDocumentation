# Operations and workflows
In the current (2022) Translator architecture, TRAPI queries are akin to database lookups: a query graph is sent as input, and knowledge satisfying that query is sent in return. Users may wish to perform subsequent operations on these results or utilize additional capabilities of Translator components besides "query lookups." The Operations and Workflow (here abbreviated with **O/W**) is designed to fulfill this purpose.

## What is a workflow?
A workflow is a sequential series of specified actions (called _operations_) that instructs Translator components exactly how to process a query. These can include actions such as sorting, filtering, adding statistical information, querying specific knowledge providers, etc. A list of currently implemented operations are given here: [List of implemented operations](http://standards.ncats.io/operation.json) and in [this part of the O/W repo](https://github.com/NCATSTranslator/OperationsAndWorkflows/tree/main/operations).

## How is an operation structured?
Operations are are structured JSON objects that are inserted into the `Workflow` section of a TRAPI message. Operations are organized into a heirarchical fashion, with most Translator components capable of executing leaf-node operations. For example, consider the `Overlay` operation: as specified in the [description](https://github.com/NCATSTranslator/OperationsAndWorkflows/blob/main/operations/overlay.yml#L3) this defines an "overlay" opperation as something that adds additional edges in the knowledge graph and/or query graph. The sub-operations define what exactly is "overlaid" on the graph. An example leaf-node sub-operation is `overlay_compute_ngd` and an example of calling it would be:
```
{"message": {
        "query_graph": {
            "nodes": {
                "n0": { "ids": [ "CHEBI:46195" ]},
                "n1": { "categories":[ "biolink:Protein" ] }
            },
            "edges": {
                "e0": { "subject": "n0",  "object": "n1" },
            }
        }
    },
"Workflow":[
    "id":"lookup,
    "id":"overlay_compute_ngd", "parameters":{"qnode_keys":["n0", "n1"], "virtual_relation_label":"NGD1"},
    "id":"bind",
    "id":"complete_results",
    "Id":"filter_results_top_n", "parameters":{"max_results": 10}]
}
```
So here the `overlay_compute_ngd` operation computes the [Normalized Google Distance](https://en.wikipedia.org/wiki/Normalized_Google_distance) between all nodes corresponding to `q_node` id `n0` and `n1` and populates this on a new edge labeled `NGD1`.  
# Using operations

# Implementing operations

# Workflow Runner

* David Koslicki?

* [Workflow Runner](https://github.com/NCATSTranslator/workflow-runner)
* [Operation and Workflow Standards](https://github.com/NCATSTranslator/OperationsAndWorkflows)
* [List of implemented operations](http://standards.ncats.io/operation.json).
