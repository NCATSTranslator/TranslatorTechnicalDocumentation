# The Translator SmartAPI Registry

The members of the Translator consortium have created many web-based Application Programming Interfaces (APIs) to share knowledgebases and tools. These are registered in the Translator SmartAPI Registry.

## SmartAPI & Translator

The SmartAPI project aims to maximize the **FAIRness** *(Findability, Accessibility, Interoperability, and Reusability)* of web-based APIs. Rich metadata is essential to properly describe an API so that it becomes discoverable, connected, and reusable. The SmartAPI metadata specification is an [OpenAPI](http://openapis.org/)-based [specification](https://github.com/SmartAPI/smartAPI-Specification/blob/OpenAPI.next/versions/3.0.0.md) that defines key API-metadata elements and value-sets. It also uses [JSON-LD](http://json-ld.org/) to provide semantically-annotated JSON content that can be treated as [Linked Data](http://linkeddata.org/). After writing a SmartAPI metadata file for an API, that file can be registered in the SmartAPI Registry to make the API discoverable and reusable for others.

**⭐ Tip:** [SmartAPI](https://smart-api.info/) provides an easy-to-use ✅ [API Metadata Editor](https://smart-api.info/editor) to quickly get started documenting your API to the latest OpenAPI v3 specification.

### Overview

Following assessments during its feasibility phase, the Biomedical Data Translator Consortium endorsed the SmartAPI Registry as the standard online registry for Translator APIs.  The resulting ✨[Translator SmartAPI Registry portal](https://smart-api.info/portal/translator) provides access to:

- The ✨[official registry of Translator tools](https://smart-api.info/registry/translator?tags=translator).
- Monitoring SmartAPI metadata files and API endpoints for changes and availability. This is to ensure that researchers have access to reliable APIs.  ℹ️ [Learn more about how SmartAPI monitors Uptime and Source Statuses.](https://github.com/SmartAPI/smartAPI/wiki/SmartAPI-Uptime-Monitoring)
- A ✨[summary dashboard](https://smart-api.info/portal/translator/summary) to view Translator APIs by:
  - Endpoint uptime (eg. 🟢 Pass, 🔴 Fail, 🟠 Unknown, 🔵 Incompatible)
  - SmartAPI file ("source") status (eg. 🟢 OK, 🟠 Not Found, 🟣 Broken, 🔴 Invalid)
  - By team, component (eg. KP, ARA)
  - Compliance with required, Translator-related SmartAPI extensions
- A ✨[Translator knowledgegraph visualizer (MetaKG)](https://smart-api.info/portal/translator/metakg) to browse and find Knowledge Provider (knowledgebase, also known as KP) APIs, based on desired relationships between biomedical entities.

### Uptime Status and Source Status Monitoring

Each API in the ✨[Translator SmartAPI Registry](https://smart-api.info/registry/translator?tags=translator) has a status badge indicating the overall status of the API based on all endpoints available for automated testing. ℹ️ [Learn more about Uptime Status on SmartAPI.](http://smart-api.info/faq#api-status)

In the event of a failure, the Registry will provide a helpful error message so you can see the reason why a particular endpoint failed the monitor check. All of this can be managed via your ✨[user dashboard](https://smart-api.info/dashboard) in the Registry.

In addition to uptime status, each entry in the registry has a "source" status badge that tracks the status of the SmartAPI metadata file. ℹ️ [Learn more about Source Status on SmartAPI.](http://smart-api.info/faq#source-status)

To see a more detailed description of how SmartAPI tracks and monitors these statuses, you can visit the ℹ️ [SmartAPI Wiki page here.](https://github.com/SmartAPI/smartAPI/wiki/SmartAPI-Uptime-Monitoring)

## Adding an API to the Translator SmartAPI Registry

First, a web-based API must be built for the knowledgebase or tool.

1. ✅ Build a REST API with JSON output (use your own preferred structure). Then work with the Service Provider team (see the "Getting Help" section below) to write and register a SmartAPI file with the extensions needed for [BioThings Explorer (BTE)](ara/bte.md) to query your API and process its output. In some cases, you may also work with BTE's team to get BTE to correctly process your API's output. This "wrapping" of your API with BTE will make your API compliant with various Translator standards (TRAPI formats and Biolink-Model semantics), which will make it usable within the Translator ecosystem of tools.
2. ✅ Build an API that is compliant with the Translator Reasoner Application Programming Interface (TRAPI) standard by following the instructions [here](trapi.md). Then write a SmartAPI file for this API and register it in the SmartAPI Registry.

Regardless of what your choice is, we recommend that you follow these ✅ [API best-practices.](https://github.com/SmartAPI/smartAPI/edit/master/docs/CREATE_API.md)

**⭐ Tip:** If you are using option 1, you may consider using the [BioThings SDK](https://docs.biothings.io/en/latest/) from the Service Provider to build your APIs. BioThings SDK will create high-quality APIs following the best practices (linked above) by default. If you need help, please ✉️ [contact the BioThings team](mailto:biothings@googlegroups.com) (also members of the "Service Provider" team in Translator).

### Translator-specific SmartAPI extensions

APIs in the Translator SmartAPI Registry must provide Translator-specific metadata in their SmartAPI metadata files.

- x-translator: global metadata for Translator project resources
- x-trapi: metadata about Translator Application Programming - Interface (TRAPI) implementations.

ℹ️ [To learn more about the Translator-specific metadata extensions used in the SmartAPI registry click here.](https://github.com/NCATSTranslator/translator_extensions).

### Registering your Translator API

To make registering a new API easier, the SmartAPI Registry provides a helpful ✨[registration guide](https://smart-api.info/guide). This guide provides helpful links to examples, tools and resources to help you write SmartAPI metadata files to document your API.

Once the SmartAPI metadata file for your API is ready, you can head over to [SmartAPI](https://smart-api.info/) and login using your **GitHub** account.  Then head over to the [Add an API](https://smart-api.info/add-api) page to register your tool.  After successfully adding your tool, it will appear on your [user dashboard](https://smart-api.info/dashboard) where you can manage anything related to your tool.

## Getting Help

The SmartAPI team is available and ready to help you with any issue. If you need to contact us please [open an issue here](https://github.com/SmartAPI/smartAPI/issues) and someone will help you ASAP!

## Tutorials

[Translator SmartAPI Registry tutorials](../guide-for-developers/tutorials/index.md)
