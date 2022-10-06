# Translator Application Programming Interface (TRAPI)

The Translator Application Programming Interface consists of two endpoint off the main server url:

- the `/meta_knowledge_graph` endpoint is a GET call that returns a list of triples in json format. 
 - The triples indicate a relationship type (`predicate`) between a subject entity type (`subject`) and an object entity type (`object`).
 - The relationship type is a selection from the [biolink predicate tree](http://tree-viz-biolink.herokuapp.com/predicates).
 - The entity type is a selection from the [biolink categories tree](http://tree-viz-biolink.herokuapp.com/categories).

- the `/query` endpoint is a POST call that expects a `query_graph` input and returns `knowledge_graph`, `query_graph` and `results` json data structures.
 - the `query_graph` input will consist of a list of triples specified by the server above.
 - the `knowledge_graph` json object consists of and `edges` map and a `nodes` map.
 - the `query_graph` json object contains the query graph serviced by the server for the request.
 - the `results` json object consists of the `node_bindings` and `edge_bindings` that describe the resulting knowledge graph relationships.

Further details can be found at [Translator Application Programming Interface (TRAPI) github](https://github.com/NCATSTranslator/ReasonerAPI).

## Tutorials

* [TRAPI tutorials](../guide-for-developers/tutorials/index.md)
