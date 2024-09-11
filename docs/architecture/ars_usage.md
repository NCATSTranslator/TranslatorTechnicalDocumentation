# Autonomous Relay System

The Autonomous Relay System (ARS) was developed by the Link Brokers team for NCATS Biomedical Data Translator

The ARS is built by NCATS staff and relays translator queries from the user to the autonomous relay agents (ARAs) using an iterative process to generate results in the form of a knowledge graph that is then provided to the user.

The ARS:

* Relays the query from the user to the ARAs
* Uses an iterative process with the ARAs to generate the result in the form of a knowledge graph provided to the user
* Decides which ARAs to invoke
* Ranks and scores answers as being most correct/relevant to the user's query

* Github Repository: [NCATSTranslator/Relay](https://github.com/NCATSTranslator/Relay)

## Team Contact: 

Mark Williams

# Interface

Access the public deployment at [https://ars-prod.transltr.io](https://ars-prod.transltr.io)

Example query to submit to the ARS at [https://ars-prod.transltr.io/ars/api/submit](https://ars-prod.transltr.io/ars/api/submit):

```
curl -X POST "https://ars.transltr.io/ars/api/submit" -H  "accept: application/json" -H  "Content-Type: application/json" -d "{
  \"message\": {
    \"query_graph\": {
      \"edges\": {
        \"e01\": {
          \"subject\": \"n0\",
          \"predicate\": \"biolink:treats\",
          \"object\": \"n1\"
        }
      },
      \"nodes\": {
        \"n0\": {
          \"category\": \"biolink:Drug\",
          \"id\": \"DRUGBANK:DB00394\"
        },
        \"n1\": {
          \"category\": \"biolink:Disease\"
        }
      }
    }
  }
}"
```

The ARS should return your query run ID:

```json
{
  "model": "tr_ars.message",
  "pk": "81a75d1d-1223-4456-8927-734ad6b600fc",
  "...": ["..."]
}
```

Results of the query can be found in the ARS messages: https://ars-prod.transltr.io/ars/api/messages

The ARAX web interface can also be used to consult the result of your query: 

1. Go to [https://arax.transltr.io/](https://arax.transltr.io/)
2. Go to the **`<id>`** tab (in **Query**)
3. Copy the run ID previously obtained in the text box
4. Click on **`Load`** to see the detailed results of your query

You can also directly access your query result by providing the run ID with the `id=` URL param: `https://arax.ncats.io/?source=ARS&id=YOUR_RUN_ID`

## Tutorials

* [Walk-through to query the ARS and retrieve results using the ARAX web interface](https://docs.google.com/document/d/1_a4gE_lY-2oZTrdFMtaZ_pxqNgd-x_1ZYI7hRGfFjng)

# Additional Resources

* [Testing Repo & NCATS standup queries/issues](https://github.com/NCATSTranslator/testing)
* [NCATS Translator GitHub Organization](https://github.com/NCATSTranslator)
* [Data Gaps](https://github.com/NCATSTranslator/DataGaps)
