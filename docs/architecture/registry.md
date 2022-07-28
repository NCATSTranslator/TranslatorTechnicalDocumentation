# TRANSLATOR & SmartAPI

### What is the Translator program

The Translator program focuses on building tools for massive knowledge integration in support of biomedical and translational science. 

The Translator program is funded through the [Cures Acceleration Network](https://ncats.nih.gov/funding/review/can "Cures Acceleration Network | National Center for Advancing Translational Sciences") (CAN). CAN is designed to advance the development of high-need cures and reduce significant barriers between research discovery and clinical trials. ℹ️ [Learn more about the Translator program here.](https://ncats.nih.gov/translator)

### Creating your Translator Tool

To create a Knowledge Provider (KP) API that's ready to be integrated into the Translator ecosystem, you can:

-  ✅ Build a REST API with JSON output (use your own preferred structure).
-  ✅ Build a ReasonerStdAPI, follow the instructions  [here](https://github.com/NCATS-Tangerine/NCATS-ReasonerStdAPI) .

Regardless of what your choice is we recommend you follow these ✅ [API best-practices.](https://github.com/SmartAPI/smartAPI/edit/master/docs/CREATE_API.md)

**⭐ Tip:** You may consider using [BioThings SDK](https://docs.biothings.io/en/latest/) to build your KP APIs. BioThings SDK will create a high-quality APIs following all these best-practices by default. If you need the help, please ✉️ [contact BioThings team](mailto:biothings@googlegroups.com)  (aka "Service Provider" KP team in Translator).

### Translator Required Extensions

Each translator tool has to adhere to a few requirements in order to recognized by the program and possibly to be integrated or ingested by other projects. 
ℹ️ [To learn more about the Translator-specific metadata extensions used in the SmartAPI registry click here.](https://github.com/NCATSTranslator/translator_extensions)

### Documenting your Translator Tool

To take full advantage of SmartAPI and make your KP API compatible with Meta-KG you will need to:

-    Create your API metadata following the latest  ✅ [OpenAPI v3 API specification](http://spec.openapis.org/oas/v3.0.3)
-   Add semantics of your API's inputs and outputs using the SmartAPI extensions.  Learn more.

**⭐ Tip:** [SmartAPI](https://smart-api.info/) provides an easy-to-use ✅ [API Metadata Editor](https://smart-api.info/editor) to quickly get started documenting your API to the latest OpenAPI v3 specification.

### What is SmartAPI

The SmartAPI project aims to maximize the **FAIRness** *(Findability, Accessibility, Interoperability, and Reusability)* of web-based Application Programming Interfaces (APIs). Rich metadata is essential to properly describe your API so that it becomes discoverable, connected, and reusable. We have developed a [](http://openapis.org/)openAPI-based [specification](https://github.com/SmartAPI/smartAPI-Specification/blob/OpenAPI.next/versions/3.0.0.md) for defining the key API metadata elements and value sets. SmartAPI's leverage the [Open API specification v3](https://www.openapis.org/) and [JSON-LD](http://json-ld.org/) for providing semantically annotated JSON content that can be treated as [Linked Data](http://linkeddata.org/).

### SmartAPI & Translator

SmartAPI serves as an online registry for Translator tools.  This registry includes monitoring of each tool's source and endpoints to help researches like you rest assured you are working with working reliable APIs.  ℹ️ [Learn more about how SmartAPI monitors Uptime and Source Statuses.](https://github.com/SmartAPI/smartAPI/wiki/SmartAPI-Uptime-Monitoring) The ✨[Translator portal](https://smart-api.info/portal/translator) on SmartAPI also includes:

 - A ✨[registry of Translator tools](https://smart-api.info/registry/translator?tags=translator).
 - A ✨[summary dashboard](https://smart-api.info/portal/translator/summary) to quickly visualize overall statuses, sources, teams, and more.
 - A ✨[knowledge graph visualizer (MetaKG)](https://smart-api.info/portal/translator/metakg) to browse and find tools based on a desired connection or relationship between biomedical entities.

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
