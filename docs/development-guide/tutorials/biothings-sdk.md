# BioThings SDK

This method is for users who have a dataset of biomedical knowledge (ex: asserting relationships between two biomedical entities) and want to build a clean and high-performance API/web service that can be used both inside AND outside of the Translator formats/ecosystem. 

## Workflow

1. use the [BioThings Software Development Kit (SDK)](https://docs.biothings.io/en/latest/index.html) to create the API (Python) - [specific instructions](https://github.com/biothings/biothings_explorer/blob/main/docs/README-contributing-new-data-source.md), [context](https://github.com/biothings/biothings_explorer/blob/main/docs/README-types-of-apis.md#biothings). For Translator, we highly prefer creating using an "association" format where each JSON document represents one relationship/edge between two biomedical entities and has `subject`, `association`, and `object` properties. The Service Provider team may help with development and deploying the API. 
2. write an SmartAPI yaml with x-bte annotation to describe this API and its data - [specific instructions](https://github.com/biothings/biothings_explorer/blob/main/docs/README-writing-x-bte.md), [json-schema](https://github.com/NCATSTranslator/translator_extensions/tree/main/x-bte). The BioThings Explorer (BTE) tool can ingest this yaml and act as a wrapper, transforming Translator-format queries (TRAPI) into corresponding queries to your API and then transforming your API's responses into Translator-format responses (TRAPI). 
   * This involves knowledge of [biolink-model](https://github.com/biolink/biolink-model), the data model the Translator consortium uses. 
   * The use of Translator NodeNormalizer (NodeNorm) and NameResolver tools can also be very useful. 
3. register this SmartAPI yaml in the [SmartAPI Registry](https://smart-api.info/), which is used by Translator to collect all tools in its ecosystem
4. contact the developer team for the BioThings Explorer (BTE) tool and ask them to add your API to their config of APIs to use. They will review your SmartAPI yaml and API and may ask for changes first. 
5. Test that you can retrieve knowledge graph (KG) edges from your dataset using BTE (direct queries). 
6. [Maintain your api and smartapi yaml](https://github.com/biothings/biothings_explorer/blob/main/docs/README-maintaining-a-data-source.md), which may involve continued communication and collaboration with BTE and Service Provider teams. 
