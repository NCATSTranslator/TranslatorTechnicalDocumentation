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

## Continuous Integration Testing

## System-Level Testing

* The [SRI Testing](sri_testing.md) and [Reasoner Validator](https://github.com/NCATSTranslator/reasoner-validator) projects cover system-level testing needs for the [Translator Reasoner Application Programming Interface (TRAPI)](https://github.com/NCATSTranslator/ReasonerAPI) and validates compliance of data flows to the [Biolink Model](https://github.com/biolink/biolink-model).

## User Interface Testing

## Quality Assurance Testing

## Customer Acceptance Testing
