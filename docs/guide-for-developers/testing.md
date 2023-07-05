# Testing within Translator

The Translator project is first and foremost, an initiative to create a novel complex software system to process biomedical knowledge. Testing of such software may be envisioned and implemented at several distinct levels:

* **[Unit Tests](#unit-testing):** code testing harnesses of granular tests embedded within a given project using well understood "best practices" applied in a computer language specific manner.
* **[Continuous integration / dev ops Testing](#continuous-integration-testing):** as distinct components of a complex multi-component system are deployed into a common environment to run as an integrated system, unit and component integration tests may be run  automatically to assess compatibility and function of the software component codee and its dependencies with the context of the common environment.
* **[System-level Testing](#system-level-testing):** Translator has evolved into a loosely-coupled web services-integrated system with shared communication syntax/semantics (i.e. TRAPI) and semantics (Biolink Model) standards for interoperability. System level testing validates component compliance with such interoperability standards.
* **[User Interface Testing](#user-interface-testing):** a software system is only ultimately as useful as the quality, fitness-of-purpose and performance of the human-machine interface. User experience testing and related methodology achieves such testing objectives.
* **[Quality Assurance Testing](#quality-assurance-testing):** again, with Translator, which is a biomedical (scientific) knowledge navigation, integration and interpretation system, "quality" refers to the scientific completeness, precision and credibility of the semantically encoded results. Tests for "Quality Assurance" may be devised to the query request/response of the system
* **[Customer Acceptance Testing](#customer-acceptance-testing):** as software system is ultimately implemented to solve "customer" (stakeholder/target end user) problems, needs and expectations. Testing such customer satisfaction is often not readily fully automated.

# Testing within Translator

## Unit Testing

A well known contemporary software development 'best practice' approach is [Test Driven Development](https://www.google.com/search?q=test+driven+development+python). A typical expression of this principle is the design of unit tests within a software project, typically using one of the diverse testing frameworks available for a given computing language, e.g. [PyTest for Python](https://docs.pytest.org/) or [JUnit for Java](https://junit.org).  The general idea is to code a unit test for as many representative use case inputs and validating outputs for the functionality of a given module, usually, its public methods constituting its interface to other parts of the system or the external user. Generally, such tests are written prior to any code being written and initially fail. Writing the code (hopefully) results in the test passing. It is often important for test inputs to probe all sensible boundary cases of possible input, to ensure functional coverage of the file.

Once such tests are written and passing, rerunning the tests after every significant revision of the application code allows for efficient detection of breaking changes including unintended secondary interactions between code sections, and provides helpful guidance for the repair of the code (or suggested revision of the unit tests themselves, if the use cases have evolved to require them).

Core Translator software applications like include unit tests for functional validation of key programmatic facets of their modules, applications like the [Biolink Model Toolkit](https://github.com/biolink/biolink-model-toolkit/tree/master/tests/unit), [KGX](https://github.com/biolink/kgx/tree/master/tests) and [reasoner-validator](https://github.com/NCATSTranslator/reasoner-validator/tree/master/tests).

Such unit tests may also be run automatically in a gatekeeper role during the commitment of code to software repositories like GitHub (i.e. using GitHub Actions), as part of the quality assurance process for releases. See [the reasoner-validator for one example of a Git Action running unit tests](https://github.com/NCATSTranslator/reasoner-validator/blob/master/.github/workflows/test.yml) in that manner.

## Continuous Integration Testing

T.B.A.

## System-Level Testing

The [Reasoner Validator](https://github.com/NCATSTranslator/reasoner-validator) projects cover system-level standards compliance testing for the [Translator Reasoner Application Programming Interface (TRAPI)](https://github.com/NCATSTranslator/ReasonerAPI) and validates compliance of data flows to the [Biolink Model](https://github.com/biolink/biolink-model).  
 
One level above the **reasoner-validator** is [SRI Testing](sri_testing.md) which attempts validation of the semantic sensitivity and specificity of knowledge graph queries, alongside compliance with TRAPI and Biolink Model standards.

## User Interface Testing

T.B.A. (A.Crouse)

## Quality Assurance Testing ("Smoke Testing")

T.B.A. - C.Bizon(?); J. Hadlow(?)

## Customer Acceptance Testing

T.B.A. (T.Beck)
