[Back to ARAs](index.md)

# BioThings Explorer Autonomous Relay Agent Page

BioThings Explorer (BTE) is an application supported by Exploring Agent. The service queries a virtual, federated knowledge graph derived from the aggregated information in a network of biomedical web services. BTE leverages semantically precise annotations of the inputs and outputs for each resource (captured in the [SmartAPI registry](https://smart-api.info/)) and automates the chaining of web service calls to execute multi-step graph queries. Because there is no large, centralized knowledge graph to maintain, BTE is distributed as a lightweight application that dynamically retrieves information at query time. More information about BioThings Explorer can be found at [https://explorer.biothings.io](https://explorer.biothings.io).

The scoring/ranking of results in BTE incorporates a number of factors, including:

- the number of paths connecting the query node to the answer node
- the length of each path
- the number of redundant paths/edges
- the provenance of the edges (e.g., text-mined versus curated)
- the [Normalized Google Distance](https://en.wikipedia.org/wiki/Normalized_Google_distance) between nodes in the path

BTE is registered on SmartAPI [here](https://smart-api.info/ui/dc91716f44207d2e1287c727f281d339). If you would like to deploy your own instance, see the [installation documentation](https://github.com/biothings/biothings_explorer/blob/main/docs/INSTALLATION.md).

## Use Cases

```sh
echo '{
  "message": {
    "query_graph": {
      "nodes": {
        "n02": {
          "categories": [
            "biolink:Disease"
          ],
          "ids": [
            "MONDO:0005148"
          ]
        },
        "n01": {
          "categories": [
            "biolink:ChemicalEntity"
          ]
        }
      },
      "edges": {
        "e01": {
          "subject": "n01",
          "object": "n02",
          "predicates": [
            "biolink:treats"
          ],
          "knowledge_type": "inferred"
        }
      }
    }
  }
}
' > creative.json

# An inferred-mode query
curl -X POST \
"https://bte.transltr.io/v1/query" \
-H "Content-Type: application/json" \
-H "accept: application/json" \
-d @creative.json
```

## Knowledge Providers Accessed

BioThings Explorer maintains a allow-list of Knowledge Providers, see [here](https://github.com/biothings/bte-server/blob/main/config/api_list.yaml).

## Source Code

[https://github.com/biothings/biothings_explorer](https://github.com/biothings/biothings_explorer) - Primary code repository for BioThings Explorer

## Additional Links

- [Exploring Agent](https://github.com/NCATSTranslator/Translator-All/wiki/Exploring-Agent/)
- Preprint: [BioThings Explorer: a query engine for a federated knowledge graph of biomedical APIs](https://arxiv.org/abs/2304.09344)
- [BioThings Explorer Home Page](https://explorer.biothings.io/)
