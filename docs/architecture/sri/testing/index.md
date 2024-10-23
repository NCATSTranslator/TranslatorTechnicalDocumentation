[Back to SRI](../index.md)
# Testing within Translator

The Translator project is first and foremost, an initiative to create a novel complex software system to process biomedical knowledge. Testing of such software may be envisioned and implemented at several distinct levels (enumerated from high-level through low-level testing):

* **[Customer Acceptance Testing](#customer-acceptance-testing):** as software system is ultimately implemented to solve "customer" (stakeholder/target end user) problems, needs and expectations. Testing such customer satisfaction is often not readily fully automated.
* **[Quality Assurance Testing](#quality-assurance-testing):** again, with Translator, which is a biomedical (scientific) knowledge navigation, integration and interpretation system, "quality" refers to the scientific completeness, precision and credibility of the semantically encoded results. Tests for "Quality Assurance" may be devised to the query request/response of the system. This kind of testing takes a variety of forms and scopes, and may be known as "smoke testing", "benchmark testing", "pass/fail testing", "quantitative testing", etc.
* **[User Interface Testing ("UI")](#user-interface-testing):** a software system is only ultimately as useful as the quality, fitness-of-purpose and performance of the human-machine interface. User experience testing and related methodology achieves such testing objectives, in addition to the "Quality Assurance" testing (above) which is directly applied through the UI.
* **[Continuous integration / Development Operations Testing](#continuous-integration-testing):** as distinct components of a complex multi-component system are deployed into a common (often, containerized) environment to run as an integrated system, unit and component integration tests may be run  automatically to assess compatibility and function of the software component code and its dependencies within the context of the common environment.
* **[System-level Testing](#system-level-testing):** Translator has evolved into a loosely-coupled web services-integrated system with shared communication syntax/semantics (i.e. TRAPI) and semantics (Biolink Model) standards for interoperability. System level testing validates component compliance with such interoperability standards. In Translator, components are also checked for their integrity of basic knowledge graph navigation performance.
* **[Unit Tests](#unit-testing):** code testing harnesses of granular tests embedded within a given project using well understood "best practices" applied in a computer language specific manner.

The details for each level of testing are as follows:

## Customer Acceptance Testing

The primary agency stakeholders, NCATS (currently, the "LinkBrokers" team in the development phase of the project), have defined the mission objectives of Translator hence are responsible to define the scope of Customer Acceptance Testing.

T.B.A. (T.Beck)

## Quality Assurance Testing

Quality Assurance Testing within Translator is being systematically designed and implemented within a [Translator Testing Infrastructure](./sri_testing_infrastructure.md) which includes a [back-end catalog of testing resources](https://github.com/NCATSTranslator/Tests) of test resources ("assets", "cases", "suites", etc.) which are imported by a Test Documentation Application and which are structured according to a formal [Testing Model Schema](https://github.com/TranslatorSRI/TranslatorTestingModel). 

An automated [Test Harness executing a diverse set of Test Runners](https://github.com/TranslatorSRI/TestHarness) is specified, with test runs and results managed by a [Test Manager](https://github.com/TranslatorSRI/TestManager) system wrapping a test results database with service API and "information radiator" UI access.

## User Interface Testing

T.B.A. (A.Crouse)

## Continuous Integration Testing

T.B.A. (Mark Williams & ITRB?)

This level of testing also includes various kinds of system monitoring using [endpoint monitoring and open telemetry](../../../deployment-guide/monitoring.md).

## System-Level Testing

The [Reasoner Validator](https://github.com/NCATSTranslator/reasoner-validator) projects cover system-level standards compliance testing for the [Translator Reasoner Application Programming Interface (TRAPI)](https://github.com/NCATSTranslator/ReasonerAPI) and validates compliance of data flows to the [Biolink Model](https://github.com/biolink/biolink-model).  
 
The tools of this System-Level testing may be run on an ad hoc basis by developers to test their compliance with Translator standards, and may also be included as a part of the Continuous Integration and the Quality Assurance levels of testing (see above)

## Unit Testing

Most software systems under development today, of practical scope, are complex.  To manage some of this complexity, a well known "best practice" is test driven development, using standard testing tools available for most computing languages, e.g. [PyTest for Python](https://docs.pytest.org/) or [JUnit for Java](https://junit.org).  Developers are generally responsible for including this level of testing directly within their individual projects.

The general idea is to code a unit test for as many representative use case inputs and validating outputs for the functionality of a given module, usually, its public methods constituting its interface to other parts of the system or the external user. Generally, such tests are written prior to any code being written and initially fail. Writing the code (hopefully) results in the test passing. It is often important for test inputs to probe all sensible boundary cases of possible input, to ensure functional coverage of the code. Once such tests are written and passed, rerunning the tests after every significant revision of the application code allows for efficient detection of breaking changes including unintended secondary interactions between code sections, and provides helpful guidance for the repair of the code (or suggested revision of the unit tests themselves, if the use cases have evolved to require them).

Core Translator software applications like include unit tests for functional validation of key programmatic facets of their modules, applications like the [Biolink Model Toolkit](https://github.com/biolink/biolink-model-toolkit/tree/master/tests/unit), [KGX](https://github.com/biolink/kgx/tree/master/tests) and [reasoner-validator](https://github.com/NCATSTranslator/reasoner-validator/tree/master/tests).

Such unit tests may also be run automatically in a gatekeeper role during the commitment of code to software repositories like GitHub (i.e. using GitHub Actions), as part of the quality assurance process for releases. See [the reasoner-validator for one example of a Git Action running unit tests](https://github.com/NCATSTranslator/reasoner-validator/blob/master/.github/workflows/test.yml) in that manner.
