# Plover

Plover is a fully **in-memory** Python-based service for hosting/serving Biolink-compliant knowledge graphs as TRAPI Knowledge Provider APIs. It's entirely **Dockerized** and doesn't use any intermediary database. 

In answering queries, Plover abides by all Translator Knowledge Provider **reasoning requirements**; it can also normalize the underlying graph and convert query node IDs to the proper equivalent identifiers for the given knowledge graph. 

**Multiple KPs** can be run on the same Plover; each is exposed at its own endpoint (see [here](https://github.com/RTXteam/PloverDB/blob/newkg2/README.md#multiple-kps) for more info).

There are two things needed to serve a KG via Plover:
1. **Nodes** and **edges** files for the graph (TSV or JSON Lines format), hosted at a publicly-accessible URL (more info [here](https://github.com/RTXteam/PloverDB/blob/newkg2/README.md#nodes-and-edges-files))
2. A Plover **config file** for the graph (more info [here](https://github.com/RTXteam/PloverDB/blob/newkg2/README.md#config-file))

The steps to then **run/deploy** Plover differ slightly depending on what you're trying to do:
1. Run Plover in a **dev fashion** (see [here](https://github.com/RTXteam/PloverDB/blob/newkg2/README.md#how-to-run-a-dev-plover))
2. Deploy a new KP on an **existing Plover** (e.g., the Multiomics Plover) (see [here](https://github.com/RTXteam/PloverDB/blob/newkg2/README.md#how-to-deploy-a-new-kp-to-an-existing-plover))
3. Deploy Plover on a **new instance** (see [here](https://github.com/RTXteam/PloverDB/blob/newkg2/README.md#how-to-deploy-plover-on-a-new-instance))

Plover automatically stands up the required TRAPI `/query` and `/meta_knowledge_graph` endpoints, as well as an endpoint that exposes SRI test triples for the KP (`/sri_test_triples`). It also provides a few other dev-oriented endpoints, described [here](https://github.com/RTXteam/PloverDB/blob/newkg2/README.md#provided-endpoints).
