# Service Provider

[Back to KPs](index.md)

Service Provider is a Translator System Knowledge Provider created by Team Service Provider with support from Team Exploring Agent. It supports queries expressed in the TRAPI format which are acyclic. Service provider leverages the BioThings API stack to build and deploy Translator KP APIs from external data sources. By registering and annotating these KP APIs in the SmartAPI registry, these KP APIs can be quickly integrated into the Translator ecosystem and used to answer the user queries. Access to Service Provider is provided through BioThings Explorer, which also acts as the Autonomous Relay Agent Exploring Agent.

## Modes of Access

- Via the Translator API (TRAPI) interface; see [the SmartAPI documentation](https://smart-api.info/ui/36f82f05705c317bac17ddae3a0ea2f0)
- Via individual BioThings APIs; see [the SmartAPI registry](https://smart-api.info/registry?tags=biothings)

### Tools and KP APIs

- **BioThings SDK**
  - **Intro:** A knowledge source KP API SDK
  - **Docs:** https://docs.biothings.io
  - **PyPI package:** https://pypi.org/project/biothings
  - **GitHub:** BioThings API

- **BioThings Studio**
  - **Intro:** A web UI for managing underlying datasource updates
  - **GitHub:** https://github.com/biothings/biothings_studio

- **SmartAPI:** https://smart-api.info
  - **Intro:** Translator's API registry
  - _Translator portal at SmartAPI_
  - **GitHub:** SmartAPI

- **MyGene.info:** https://mygene.info
  - **Intro:** A gene-centric knowledge KP
  - **Docs:** https://docs.mygene.info
  - **GitHub:** MyGene.info

- **MyVariant.info:** https://myvariant.info
  - **Intro:** A genetic variant-centric KP
  - **Docs:** https://docs.myvariant.info
  - **GitHub:** MyVariant.info

- **MyChem.info:** https://mychem.info
  - **Intro:** A drug and chemical-centric KP
  - **Docs:** https://docs.mychem.info
  = **GitHub:** MyChem.info

- **MyDisease.info:** https://mydisease.info
  - **Intro:** A disease and phenotype-centric KP
  - **Docs:** https://docs.mydisease.info
  - **GitHub:** MyDisease.info

All other KPs hosted at: https://biothings.ncats.io

Live Translator 'Meta Knowledge Graph' (MetaKG): https://smart-api.info/api/metakg

Issues using Service Provider should be logged in the [BioThings Explorer issue tracker](https://github.com/biothings/biothings_explorer)

## Use Cases

One-hop query:

```sh
echo '{
  "message": {
    "query_graph": {
      "nodes": {
        "sn": { "categories": ["biolink:SmallMolecule"] },
        "on": { "categories": ["biolink:Gene"], "ids": ["NCBIGene:154"] }
      },
      "edges": {
        "e1": {
          "subject": "sn",
          "object": "on",
          "predicates": ["biolink:affects"]
        }
      }
    }
  }
}' > onehop.json

# To all of Service Provider
curl -X POST \
"https://bte.transltr.io/v1/team/service-provider/query" \
-H "Content-Type: application/json" \
-H "accept: application/json" \
-d @onehop.json

# To a specific Service Provider BioThings API
# For this example, BioThings DGIdb
curl -X POST \
"https://bte.transltr.io/v1/smartapi/e3edd325c76f2992a111b43a907a4870/query" \
-H "Content-Type: application/json" \
-H "accept: application/json" \
-d @onehop.json
```

Other Translator KP APIs Powered by BioThings SDK

## Knowledge Sources Accessed

[Aeolus](https://www.nature.com/articles/sdata201626) (MyChem) • [agrkb](https://www.alliancegenome.org/downloads) (BioThings AGR) • [bindingdb](https://www.bindingdb.org/rwd/bind/index.jsp) (BioThings BindingDB) • [bioplanet](https://tripod.nih.gov/bioplanet/#) (BioThings Bioplanet Pathway-Disease and Pathway-Gene APIs) • Chebi xrefs to reactome and rhea (MyChem) • Chembl (MyChem) • [CIViC](https://civicdb.org/welcome) (MyVariant) • [ClinGen](https://www.clinicalgenome.org/) (MyGene) • [Clinvar](https://www.ncbi.nlm.nih.gov/clinvar/) (MyVariant) • [complex-portal](https://www.ebi.ac.uk/complexportal/home) (ComplexPortal's API) • [ConsensusPathDB](http://cpdb.molgen.mpg.de/) (MyGene) •  [CTD's API](https://ctdbase.org/help/linking.jsp#batchqueries) (MyDisease) • dbsnp (MyVariant) • [ddinter](http://ddinter.scbdd.com/) (BioThings DDInter) • [dgidb](https://dgidb.org/) (BioThings DGIdb) • [DISEASES](https://diseases.jensenlab.org/About) (BioThings DISEASES) • [disgenet](https://www.disgenet.org/) (MyDisease) • [Drugcentral](https://drugcentral.org/) (MyChem) • [EBI gene2phenotype](https://www.ebi.ac.uk/gene2phenotype/) (BioThings EBIgene2phenotype) • [FDA orphan drug data](https://www.accessdata.fda.gov/scripts/opdlisting/oopd/) (MyChem) • FooDB (BioThings FooDB) • FoodData Central (BioThings FoodData Central) • GO (BioThings GO Biological Process, BioThings GO Cellular Component, BioThings GO Molecular Function) • GO annotations - [NCBI Gene](https://www.ncbi.nlm.nih.gov/gene) (MyGene) • [GTRx](https://gtrx.rbsapp.net/about.html) (BioThings GTRx) • HPO (BioThings HPO) • HPO Annotations (MyDisease, BioThings HPO) • [iDISK](https://pubmed.ncbi.nlm.nih.gov/32068839/) (BioThings IDISK) • [InnateDB](https://www.innatedb.com/) (BioThings InnateDB) • [MGI gene-disease/gene-phenotype info](https://www.informatics.jax.org/humanDisease.shtml) (BioThings MGI gene2phenotype) • monarchinitiative (Monarch API) • mondo (MyDisease) • [NCATS RARe-SOURCE](https://raresource.nih.gov/) (BioThings RARe-SOURCE) • [Panther](https://pantherdb.org/) (MyGene) • [pfocr](https://pfocr.wikipathways.org/) (BioThings PFOCR) • reactome (MyGene) • repoDB (BioThings repoDB API) • [rhea](https://www.rhea-db.org/) (BioThings Rhea) • semmeddb (BioThings SEMMEDDB) • [suppKG](https://doi.org/10.1016/j.jbi.2022.104120) (BioThings suppKG) • [TTD](https://db.idrblab.net/ttd/) (BioThings TTD) • [uberon](https://obophenotype.github.io/uberon/about/) (BioThings UBERON) • **uniprot** gene -> rhea reaction mapping (through [EBI Proteins API](https://www.ebi.ac.uk/proteins/api/doc/))

## External Documentation

- [Service KP Milestone Dashboard](https://github.com/orgs/biothings/projects/5)

- [BioThings SDK/Studio documentation](https://docs.biothings.io/en/latest/tutorial/studio.html)
