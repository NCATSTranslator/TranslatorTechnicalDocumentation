# The Translator Smart-API Registry

A central resource of the Translator platform is an online registry of knowledge provider and graph integration web service components ('tools'). This resource is the Translator Registry, based on the SmartAPI framework (the "Translator Smart-API Registry").

### What is SmartAPI

The SmartAPI project aims to maximize the **FAIRness** *(Findability, Accessibility, Interoperability, and Reusability)* of web-based Application Programming Interfaces (APIs). Rich metadata is essential to properly describe your API so that it becomes discoverable, connected, and reusable. We have developed a [](http://openapis.org/)openAPI-based [specification](https://github.com/SmartAPI/smartAPI-Specification/blob/OpenAPI.next/versions/3.0.0.md) for defining the key API metadata elements and value sets. SmartAPI's leverage the [Open API specification v3](https://www.openapis.org/) and [JSON-LD](http://json-ld.org/) for providing semantically annotated JSON content that can be treated as [Linked Data](http://linkeddata.org/).

### SmartAPI & Translator

Following assessments during its feasibility phase, the Biomedical Data Translator Consortium endorsed the SmartAPI as their standard online registry for Translator web service based components ('tools').  The resulting ✨[Translator SmartAPI Registry portal](https://smart-api.info/portal/translator) provides access to:
 - The ✨[official registry of Translator tools](https://smart-api.info/registry/translator?tags=translator).
 - Realtime monitoring and compliance to SmartAPI standards, of each tool's source and endpoints, to ensure that researchers have access to reliable APIs.  ℹ️ [Learn more about how SmartAPI monitors Uptime and Source Statuses.](https://github.com/SmartAPI/smartAPI/wiki/SmartAPI-Uptime-Monitoring) 
 - A ✨[summary dashboard](https://smart-api.info/portal/translator/summary) to quickly visualize overall statuses, sources, teams, and more.
 - A ✨[Translator knowledge graph visualizer (MetaKG)](https://smart-api.info/portal/translator/metakg) to browse and find tools based on a desired connection or relationship between biomedical entities.

### Adding a Knowledge Provider to Translator

To publish a Knowledge Provider (KP) API that's ready to be integrated into the Translator ecosystem, you can:

1.  ✅ Directly register your own OpenAPI web service implementation (with its own custome endpoints and JSON output data models) in the SmartAPI Registry, to be generically accessed by the [BioThings Explorer (BTE)](ara/bte.md).
2.  ✅ Directly wrap your knowledge source with a standard Translator Reasoner Application Programming Interface (TRAPI), follow the instructions [here](trapi.md) .

Regardless of what your choice is we recommend you follow these ✅ [API best-practices.](https://github.com/SmartAPI/smartAPI/edit/master/docs/CREATE_API.md)

**⭐ Tip:** If you wish to have the benefits of option 2 above, by leveraging your existing investment in custom OpenAPI web service design, you may consider using [BioThings 'Service Provider' SDK](https://docs.biothings.io/en/latest/) wrap your custom KP API with TRAPI. BioThings SDK will create a high-quality APIs following all these best-practices by default. If you need the help, please ✉️ [contact BioThings team](mailto:biothings@googlegroups.com)  (aka the "Service Provider" KP team in Translator).

### Documenting your Translator Tool

To take full advantage of SmartAPI and make your KP API compatible with Translator Meta-KG, you will generally need to:

-   Create your API metadata following the latest  ✅ [OpenAPI v3 API specification](http://spec.openapis.org/oas/v3.0.3)
-   Document the semantics of your API's inputs and outputs by implementing a Biolink Model compliance knowledge map of your tool (generally by implementing the [TRAPI **`/meta_knowledge_graph`** endpoint](https://github.com/NCATSTranslator/ReasonerAPI/blob/master/TranslatorReasonerAPI.yaml#L73) or by curating the equivalent metadata for BTE or the Service Provider using the SmartAPI extensions)

Note that SmartAPI registration of a web service application specifically for Translator also has to adhere to a few SmartAPI extension requirements in order to recognized by the Translator platform, for possible integration with other Translator components. ℹ️ [To learn more about the Translator-specific metadata extensions used in the SmartAPI registry click here.](https://github.com/NCATSTranslator/translator_extensions).

**⭐ Tip:** [SmartAPI](https://smart-api.info/) provides an easy-to-use ✅ [API Metadata Editor](https://smart-api.info/editor) to quickly get started documenting your API to the latest OpenAPI v3 specification.

### Registering your Translator Tool on SmartAPI

To make registering a new tool easier SmartAPI provides a helpful ✨[registration guide](https://smart-api.info/guide). This guide provides helpful links to examples, tools and resources to help you document your API.

Once done you can head over to [SmartAPI](https://smart-api.info/) and login using your **GitHub** account.  Then simply head over to the [Add an API](https://smart-api.info/add-api) page to register your tool.  After successfully adding your tool, it will appear on your [user dashboard](https://smart-api.info/dashboard) where you can manage anything related to your tool. 

### Translator Tool Registry

The ✨[Translator tool registry](https://smart-api.info/registry/translator?tags=translator) on SmartAPI shows you all the currently available tools by all the teams on this program. Powered by a powerful ✨[BioThings API](https://biothings.io/) this registry can handle complex and sophisticated queries to quickly find relevant tools, or simply filter by TRAPI version, component or teams.

### Summary of Translator tools

The ✨[Translator summary dashboard](https://smart-api.info/portal/translator/summary) visualizes various properties across all Translator tools such as:

 - Endpoint uptime (eg. 🟢 Pass, 🔴 Fail, 🟠 Unknown, 🔵 Incompatible)
 - Original source status (eg. 🟢 OK, 🟠 Not Found, 🟣 Broken, 🔴 Invalid)
 - Tools by team, component, etc. (eg. KP, ARA)
 - Translator and TRAPI compliance such as required translator extensions. 

### Uptime Status and Source Status Monitoring

Each tool on the ✨[Translator tool registry](https://smart-api.info/registry/translator?tags=translator) has a status badge indicating the overall assigned status based on all the endpoints available for testing. ℹ️ [Learn more about Uptime Status on SmartAPI.](http://smart-api.info/faq#api-status)

In the event of a failure SmartAPI will provide a helpful error message so you can see the reason why any particular endpoint failed the monitor check. All of this can be managed via your ✨[user dashboard](https://smart-api.info/dashboard) on SmartAPI.

In addition to the uptime status, each hit on the registry also has a source status badge that tracks the status of the original metadata URL.  ℹ️ [Learn more about Source Status on SmartAPI.](http://smart-api.info/faq#source-status)

To see a more detailed description of how SmartAPI tracks and monitors these statuses you can visit the ℹ️ [SmartAPI Wiki page here.](https://github.com/SmartAPI/smartAPI/wiki/SmartAPI-Uptime-Monitoring)

### Getting Help

  The SmartAPI team is available and ready to help you with any issue. If you need to contact us please [open an issue here](https://github.com/SmartAPI/smartAPI/issues) and someone will help you ASAP! 

* [Translator Extensions](https://github.com/NCATSTranslator/translator_extensions)
  * **x-translator**: global metadata for Translator project resources
  * **x-trapi**: metadata about [Translator Application Programming Interface (TRAPI)](https://github.com/NCATSTranslator/ReasonerAPI) implementations.

## Tutorials

* [Translator SmartAPI Registry tutorials](../guide-for-developers/tutorials/index.md)
