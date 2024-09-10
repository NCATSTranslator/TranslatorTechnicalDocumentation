# What I want to know is...

### How do I find an identifier for a biomedical concept/entity?
CURIE's (Compact Uniform Resource Identifiers) are used in TRAPI messages to identify particular biomedical objects and concepts. 
Here are two ways to convert from natural language to a CURIE:

1. The [SRI Name Resolver](https://name-resolution-sri.renci.org/docs), specifically the `/lookup` endpoint, can take natural language and find a CURIE associated with it.
2. The [ARAX UI](https://arax.transltr.io/) has a `Synonyms` feature on the left bar under the heading `Tools`. In it, you can type a term (with autocomplete) and find equivalent CURIES. This approach uses both the SRI Name Resolver and additional information derived from RTX-KG2.


### How do I compute the Normalized Google Distance (NGD) between two concepts
The endpoint [https://arax.transltr.io/api/arax/v1.4/ui/#/PubmedMeshNgd/pubmed_mesh_ngd](https://araxtransltr.io/api/arax/v1.4/ui/#/PubmedMeshNgd/pubmed_mesh_ngd) takes two natural language inputs (terms occurring in UMLS) and returns the NGD between them.


### How can I quickly view a TRAPI response?
The ARAX UI [https://arax.transltr.io/](https://arax.transltr.io/) can take a TRAPI response <img src="https://github.com/user-attachments/assets/780025a6-9907-4802-87ba-238896c002a5" width="150"> and render the results. This is mainly helpful for debugging and development use. You can also enter a PK in the ID field <img src="https://github.com/user-attachments/assets/c3cdda80-9790-4324-99a8-057bb9a84202" width="150">.

