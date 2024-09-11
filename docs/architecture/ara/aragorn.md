[Back to ARAs](index.md)

# Aragorn Autonomous Relay Agent Page

Autonomous Relay Agent for Generation Of Ranked Networks (ARAGORN) is an autonomous relay agent support by the ranking ragent team. Aragorn operates in a federated knowledge environment and queries all known Knowledge Providers (KPs) found in the [SmartAPI registry](https://smart-api.info/). 

Aragorn processes data using a collection of supporting services also managed by the ranking agent team:

* [Strider](https://github.com/ranking-agent/strider) - Responsible for federated querying of known KPs, normalizing identifiers using the Node Normalizer, and formating results.
* [Omnicorp](https://github.com/ranking-agent/aragorn-ranker/blob/master/ranker/modules/omnicorp_overlay.py) - Responsible for annotating nodes and edges with literature co-occurence information to support ranking.
* [Aragorn Ranker](https://github.com/ranking-agent/aragorn-ranker) - Responsible for ranking results using available meta-data information and an algorithm inspired by information flow.

In addition, Aragorn contains algorithms to orchestrate these services to support inferred edges, set-input queries, and path queries.

## Inferred Edges
Aragorn uses a collections of rules learned using AMIE+ on the Robokop graph to expand an inferred query edge into a collection of non-inferred queries. Each of these queries is then sent to Strider. Aragorn then merges the set of results and formats the results, before completing ranking.

## Set-Input Queries
Set-Input queries are primarily handled in Strider.

## Implementation
Aragorn is asynchronous with requests to supporting services called in an asynchronous manner with callback URLs. Redis is used to handle communication between worker threads to ensure that requests are available despite any difference from the initiating worker.

## Ranking
The Aragorn ranking algorithm transforms a set of known attributes into measures between 0 and 1, and then uses these measures to model flow of information between sets of nodes. An algorithm is used to identify which nodes should be measured (probes) using the query graph connectivity and specificity. Thanking algorithm also transforms weights in the range of [0, 1] to ensure that the resulting effective weight between any two prob nodes remains in the scale of [0, 1]. The ranking algorithm operates on arbitrary graph shapes and does not directly penalize for path length, result graph structure or query structure. A full list of attributes and how they are transformed for ranking is available in the [Aragron ranker source code](https://github.com/ranking-agent/aragorn-ranker/blob/master/ranker/shared/sources.py).

## Additional Links

- [Ranking Agent](https://github.com/NCATSTranslator/Translator-All/wiki/Ranking-Agent/)
