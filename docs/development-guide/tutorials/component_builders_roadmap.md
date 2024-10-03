# A Translator Component Builder's Road Map

The Phase 2 - Development projects of Translator created a cluster of KP and ARA components, queried by the ARS.  Knowledge coverage was constrained to a priority set of knowledge sources highlighted by Phase 2 teams, but obviously, don't completely reflect every knowledge sources nor knowledge graph processing strategy imaginable. The need to integrate such novel resources into Translator suggest the need to develop and integrate novel KP, ARA or utility components in the platform.

In addition, future development of Translator (e.g. Phase 3 - Performance, starting _circa_ December 2024) will likely draw in new teams and their developers, interested in contributing to the platform, hence, needing a clear starting point to get up to speed on component development.  

Even with Phase 2 project teams, already familiar with the platform, the maintenance of Translator components will sometimes run up against the challenge of complexity of the Translator platform thus, highlighting an ongoing need to refresh knowledge about platform standards,  available software and best practices relating to those components.

The purpose of this document is to provide a concrete one-stop, step-by-step road map about component design and implementation which serves all the above development needs.

## Resources

For data owners who would like to make their data accessible within Translator as Knowledge Providers, there are several turnkey options to consider:

* [BioThings SDK](biothings-sdk.md): good for creating JSON-based REST APIs that can be semantically annotated using the SmartAPI x-bte standard.
* [Plater](https://github.com/TranslatorSRI/Plater): good for wrapping a local Neo4j database loaded with Biolink Model compliant knowledge graph(s).
* [PLOVER](plover.md): serves _in-memory_ hosted Biolink Model compliant datasets, without the complication of maintaining a backend graph database.

To better understand the various standards and component facets, or perhaps, roll-your-own Translator component from scratch, the following topics should be reviewed:

* [Biolink Model](https://biolink.github.io/biolink-model/working-with-the-model/)
* [Implementing TRAPI](https://github.com/NCATSTranslator/ReasonerAPI/tree/master/ImplementationGuidance)
* [Specifying Workflows](workflows.md)
* [Deploying a Translator Component](../../deployment-guide/index.md)
* [Registering a TRAPI service](../../architecture/registry.md#adding-an-api-to-the-translator-smartapi-registry)
