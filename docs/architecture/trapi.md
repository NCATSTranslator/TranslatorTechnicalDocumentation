# Translator Reasoner Application Programming Interface

The Translator strives to navigate, integrate, and interpret statements of biomedical knowledge ("KGs") consisting of concepts ("nodes") linked by their predicate relationships ("edges"). Such knowledge is standardized and made visible by wrappers ("KPs") of third-party sources, for access by computational engines ("ARAs"), thus providing value-added reasoning. 

Although some such components and knowledge graphs are amenable to centralized solutions, a more general solution to the task is the creation of a standardized network of commuication across distinct, distributed KPs and ARAs, with knowledge queries orchestrated within [workflows](workflows.md). In Translator, this is the goal of the Translator Reasoner Application Programming Interface (TRAPI).

TRAPI defines a standard HTTP web service API for communicating biomedical questions and answers. It leverages the standards of the  [Biolink model](https://biolink.github.io/biolink-model/) to precisely describe the semantics of biological entities and relationships. TRAPI's graph-based query-knowledge-binding structure enables expressive yet concise description of biomedical questions and answers.

TRAPI is described primarily by an [OpenAPI](https://github.com/OAI/OpenAPI-Specification) document [here](https://github.com/NCATSTranslator/ReasonerAPI/blob/master/TranslatorReasonerAPI.yaml). The request/response structure is also documented in a more human-readable form [here](https://github.com/NCATSTranslator/ReasonerAPI/blob/master/docs/reference.md).

TRAPI consists of two endpoints off the main server url:

# The /meta_knowledge_graph Endpoint

- the `/meta_knowledge_graph` endpoint is a GET call that returns a list of triples in json format. 
- The triples indicate a relationship type (`predicate`) between a subject entity type (`subject`) and an object entity type (`object`).
- The relationship type is a selection from the [biolink predicate tree](http://tree-viz-biolink.herokuapp.com/predicates).
- The entity type is a selection from the [biolink categories tree](http://tree-viz-biolink.herokuapp.com/categories).

# The /query Endpoint

- the `/query` endpoint is a POST call that expects a `query_graph` input and returns `knowledge_graph`, `query_graph` and `results` json data structures.
- the `query_graph` input will consist of a list of triples specified by the server above.
- the `knowledge_graph` json object consists of and `edges` map and a `nodes` map.
- the `query_graph` json object contains the query graph serviced by the server for the request.
- the `results` json object consists of the `node_bindings` and `edge_bindings` that describe the resulting knowledge graph relationships.

TRAPI queries are also structured and guided by the context of [knowledge workflows](workflows.md).

Further details can be found at [Translator Application Programming Interface (TRAPI) github](https://github.com/NCATSTranslator/ReasonerAPI).

## Tutorials

* [TRAPI tutorials](../guide-for-developers/tutorials/index.md)
