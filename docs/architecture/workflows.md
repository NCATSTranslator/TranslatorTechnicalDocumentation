# Operations and workflows
In the current (2022) Translator architecture, TRAPI queries are akin to database lookups: a query graph is sent as input,
and knowledge satisfying that query is sent in return. Users may wish to perform subsequent operations on these results 
or utilize additional capabilities of Translator components besides "query lookups." The Operations and Workflow (here 
abbreviated with **O/W**) is designed to fulfill this purpose.

## What is a workflow?
A workflow is a sequential series of specified actions (called _operations_) that instructs Translator components 
exactly how to process a query. These can include actions such as sorting, filtering, adding statistical information, 
querying specific knowledge providers, etc. A list of currently implemented operations are given here: 
[List of implemented operations](http://standards.ncats.io/operation.json) and in 
[this part of the O/W repo](https://github.com/NCATSTranslator/OperationsAndWorkflows/tree/main/operations).

## How is an operation structured?
Operations are structured JSON objects that are inserted into the `Workflow` section of a TRAPI message. Operations 
are organized into a hierarchical fashion, with most Translator components capable of executing some leaf-node operations. 
For example, consider the `Overlay` operation: as specified in the 
[description](https://github.com/NCATSTranslator/OperationsAndWorkflows/blob/main/operations/overlay.yml#L3) this 
defines an "overlay" operation as something that adds additional edges in the knowledge graph and/or query graph. The 
sub-operations define what exactly is "overlaid" on the graph. An example leaf-node subclass operation is 
`overlay_compute_ngd` and an example of calling it would be:
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
So here the `overlay_compute_ngd` operation computes the 
[Normalized Google Distance](https://en.wikipedia.org/wiki/Normalized_Google_distance) 
between all nodes corresponding to `q_node` id `n0` and `n1` and populates this on a new edge labeled `NGD1`. 

Operations have a variety of properties, including input requirements, output guarantees, allowed changes, and parameters.

Importantly, operations that have the `unique: true` property are expected to result in different behavior depending on 
which Translator component the operation is sent to. For example, the `fill` operation populates a knowledge graph with 
bioentities that satisfy an input query graph. It is assumed that different components can fill different kinds of knowledge, 
so this operation has the `unique: tree` property. Other operations (such as some sorting operations) have `unique: false` since each 
component is expected to perform the operation in the same fashion.

### Compound operations
For convenience, some operations are compositions of a number of other operations. For example, [lookup_and_score](https://github.com/NCATSTranslator/OperationsAndWorkflows/blob/main/operations/lookup_and_score.yml) 
is the composition of the operations `fill`, `bind`, `complete_results`, and `score`. These operations act identically 
as to sequentially executing the sub-operations that comprise it.

# Using operations

A TRAPI query that utilizes the O/W language may or may not have a populated query graph and/or knowledge graph. For example, 
a `fill` operation may only have a populated query graph, while a `filter` operation may have a populated query graph 
and knowledge graph.

Typically, if you are starting with a "fresh" query, the usual procedure is as follows:

- Provide a query graph and empty knowledge graph, and populate the `Workflow` portion of the TRAPI query with the following operations:
  - `fill` this will instruct Translator components to find knowledge that satisfies the query graph (akin to a database lookup)
  - Any of the `annotate`, `filter`, or `overlay` operations to argument the knowledge with additional information, filter 
out some bioentities, etc.
  - `bind` and `complete_results` as this will form the answer set for the query
  - Additional `sort` or `filter` operations as desired.

A "standard" TRAPI query (without a workflow) is equivalent to sending a query graph and calling `lookup_and_score` 
as this will only find bioentities that satisfy a query graph, score/rank the results, and return it to a user.

More complicated workflows can be created by mixing and matching the above typical procedure. For example, 
[here](https://gist.github.com/dkoslicki/44c3352a2b86d214e4fe104e5ab2ac47) is a workflow that:

- Reaches out to COHD to find the first hop of a query
- Overlays the Normalized Google Distance
- Takes the top three highest scoring results
- Reaches out to a different KP to find two subsequent hops that optionally:
  - are either `increases_activity_of` and `increases_activity_of`
  - or `decreases_activity_of` and `decreases_activity_of` (i.e. same direction of activity)
- Create and rank the final answers

In this fashion, a user can precisely specify what sort of workflow they desire.

# Advertising operations
Each Translator component is expected to implement a set of operations that it can perform. This is done via 
the OpenAPI specification utilizing the `x-trapi` extension. Directions on how to implement this can be found
[here](https://github.com/NCATSTranslator/OperationsAndWorkflows/wiki/How-to-%22do%22-operations#advertising-operations)
 with a real-world example [here](https://arax.ncats.io/test/api/arax/v1.2/openapi.json).

# Implementing operations
Please see the [Guide for developers](../guide-for-developers/tutorials/workflows.md) for developer details about how 
to implement new operations.

# Operations and workflow policies
In the current architecture, Translator components are expected to perform the operations in the order they are 
specified in the `workflow` section of a TRAPI message. This is a strict requirement, and if a component encounters 
an operation it has not implemented, it must throw an error. No additional operations or actions are to be performed 
besides that which is specified in the `workflow` section.

Each Translator ARA is required to at minimum implement the `lookup` and/or `lookup_and_score` operations. These are 
equivalent to a standard TRAPI query without the `workflow` section. KP's can optionally implement these operations.

Translator components are encouraged to create PRs to implement additional operations. This is a mechanism 
by which components can expose additional functionality that may not currently fit in the "non-workflow" TRAPI paradigm.

# Workflow Runner
The workflow runner is a component that is responsible for identifying which Translator components can execute the 
specified operations in a workflow, sending the TRAPI message to those components, and then combining and returning the results. 
The figure below depicts the architecture of the workflow runner and how it is related to the ARS and ARAs. Note 
that the workflow runner is a component that is not a part of the ARS or ARAs, but is instead a component that is that sits 
between the ARS and ARAs/KPs. Thought it is not shown here, any KP can also advertise operations it can perform (as described 
above) and the workflow runner will query these KPs if given a workflow with the relevant operation.

<img width="841" alt="Screen Shot 2022-06-24 at 3 58 12 PM" src="https://user-images.githubusercontent.com/6362936/175659052-4b0b12c3-1e03-4715-ac0e-540dd6d2144a.png">

If the workflow runner is unable to find a component that can perform the operation, it will throw an error. 
When the workflow runner is given a workflow, it will iterate through the operations in the workflow and:
- If the operations is marked as `unique: true`, it will send the TRAPI message to all component(s) that implements that operation
- If the operations is marked as `unique: false`, it will send the TRAPI message to a single component that implement that operation

After each operation is executed, the results are combined before executing subsequent operations.

# Additional links
* [Workflow Runner](https://github.com/NCATSTranslator/workflow-runner)
* [Operation and Workflow Repo](https://github.com/NCATSTranslator/OperationsAndWorkflows)
* [List of implemented operations](http://standards.ncats.io/operation.json)
