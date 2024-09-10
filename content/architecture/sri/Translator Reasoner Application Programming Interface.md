Translator strives to navigate, integrate, and interpret statements of biomedical knowledge ("KGs") consisting of concepts ("nodes") linked by their predicate relationships ("edges"). Such knowledge is standardized and made visible by wrappers ("KPs") of third-party sources, for access by computational engines ("ARAs"), thus providing value-added reasoning.

Although some such components and knowledge graphs are amenable to centralized solutions, a more general solution to the task is the creation of a standardized network of communication across distinct, distributed KPs and ARAs, with knowledge queries orchestrated within [Operations and Workflows](Operations%20and%20Workflows.md). In Translator, this is the goal of the Translator Reasoner Application Programming Interface (TRAPI).

TRAPI defines a standard HTTP web service API for communicating biomedical questions and answers. It leverages the standards of the  [Biolink model](https://biolink.github.io/biolink-model/) to precisely describe the semantics of biological entities and relationships. TRAPI's graph-based query-knowledge-binding structure enables expressive yet concise description of biomedical questions and answers.

TRAPI is described primarily by an [OpenAPI](https://github.com/OAI/OpenAPI-Specification) document [here](https://github.com/NCATSTranslator/ReasonerAPI/blob/master/TranslatorReasonerAPI.yaml). The request/response structure is also documented in a more human-readable form [here](https://github.com/NCATSTranslator/ReasonerAPI/blob/master/docs/reference).

TRAPI consists of two endpoints off the main server url:

# The /meta_knowledge_graph Endpoint

- The `/meta_knowledge_graph` endpoint responds to a GET call to return a list of the types of triples in json format that are supported by the KP or ARA. For example, if the KP has instances of triples corresponding to the type Drug-treats-Disease, the `/meta_knowledge_graph` endpoint response will include Drug-treats-Disease.
- The triples indicate a relationship type (`predicate`) between a subject entity type (`subject`) and an object entity type (`object`).
- The relationship type is a selection from the [biolink predicate tree](http://tree-viz-biolink.herokuapp.com/predicates).
- The entity type is a selection from the [biolink categories tree](http://tree-viz-biolink.herokuapp.com/categories).

# The /query Endpoint

- The `/query` endpoint expects a POST of a TRAPI document that contains a `query_graph`. The response is another TRAPI document that contains `knowledge_graph`, the original `query_graph`, and `results` json data structures.
- The `query_graph` input encode the question being asked in the form of a graph.
- The `knowledge_graph` json object consists of an `edges` map and a `nodes` map.
- The `query_graph` json object contains the query graph serviced by the server for the request.
- The `results` json object consists of the `node_bindings` and `edge_bindings` that describe the resulting knowledge graph relationships.

TRAPI queries are also structured and guided by the context of [Operations and Workflows](Operations%20and%20Workflows.md).

Further details can be found at [TRAPI github](https://github.com/NCATSTranslator/ReasonerAPI).

## Tutorials

* [[../../development-guide/tutorials/index|TRAPI tutorials]]
