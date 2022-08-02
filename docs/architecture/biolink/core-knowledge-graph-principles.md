# Knowledge graphs and why they're used in Translator

## What are knowledge graphs?

Within clinical, biomedical, and translational science, an increasing number of projects are adopting graphs for knowledge representation.
Graph-based data models such as knowledge graphs (KGs) elucidate the interconnectedness between core biomedical concepts, enable data structures to be easily updated,
and support intuitive queries, visualizations, and inference algorithms.
In a KG, entities or data types are represented as nodes and connected to each other by edges with predicates that describe the relationship between entities.
A “schema” is used to constrain the KG by specifying how knowledge can be represented;
as such, it provides a framework for validating specific instances of knowledge representation through rules that dictate the syntax and semantics.
KGs allow users to pose questions that can then be translated into query graphs and applied to identify subgraphs within the KG that match the general structure of the query graph, thereby producing answers to user queries and generating new knowledge.

## Why does Translator use knowledge graphs?
The Translator Consortium has adopted a federated KG-based approach for biomedical knowledge representation and discovery.
Using KGs enables Translator to integrate a wide range of heterogeneous data sets and translate them into insights intended to augment human reasoning
and accelerate translational science.
For more about Translator and how it uses KGs, please see the [2022 Translator paper](https://ascpt.onlinelibrary.wiley.com/doi/10.1111/cts.13301), reference 1 below).

## What is Biolink Model?
[Biolink Model](https://github.com/biolink/biolink-model) is an open source data model that can be used to formalize
the relationships between data structures in translational science.
It incorporates object-oriented classification and graph-oriented features.
The core of the model is a set of hierarchical, interconnected classes (or categories) and relationships between them (or predicates),
representing biomedical entities such as gene, disease, chemical, anatomical structure, and phenotype.
The model provides class and edge attributes and associations that guide how entities should relate to one another.
For more info about Biolink Model, please see the [Biolink Model paper](https://onlinelibrary.wiley.com/doi/10.1111/cts.13302) and [Biolink documentation](https://biolink.github.io/biolink-model/) (references 2 and 3 below).

## What role does Biolink Model play in Translator?
The Translator Consortium uses Biolink Model as an upper-level graph-oriented universal schema that supports semantic harmonization and reasoning
across diverse Translator knowledge sources.
In order to interoperate between knowledge sources and reason across KGs, Biolink Model was adopted by Translator as the common dialect
to provide rich annotation metadata to the nodes and edges in disparate graphs, thus enabling queries over the entire Translator KG ecosystem,
despite incompatibilities in the underlying data sources.
The result is a federated, harmonized ecosystem that supports advanced reasoning and inference to derive biomedical insights based on user queries.

References:
1. Fecho K, Thessen AT, et al. and The Biomedical Data Translator Consortium.
Progress Toward a Universal Biomedical Data Translator. Clin Transl Sci. Wiley Online Library; 2022 May 25;
[http://dx.doi.org/10.1111/cts.13301](http://dx.doi.org/10.1111/cts.13301)

2. Unni DR, Moxon SAT, et al. and The Biomedical Data Translator Consortium.
Biolink Model: A universal schema for knowledge graphs in clinical, biomedical, and translational science.
Clin Transl Sci. Wiley; 2022 Jun 6; [https://onlinelibrary.wiley.com/doi/10.1111/cts.13302](https://onlinelibrary.wiley.com/doi/10.1111/cts.13302)

3. [Biolink Model documentation](https://biolink.github.io/biolink-model/)
