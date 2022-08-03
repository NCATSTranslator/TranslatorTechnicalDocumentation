# SRI Testing Harness

The [SRI Testing Harness](https://github.com/TranslatorSRI/SRI_testing) is a software testing system for the validation of TRAPI-wrapped Translator Knowledge Provider ("KP") and Autonomous Relay Agents ("ARA") components.

## Scope

The framework uses Biolink Model compliant sample 'edge' test data hosted online (see ['Specifying the Tests'](#specifying-the-tests) below) as curated for each target KP, plus configuration information for associated Autonomous Relay Agents ("ARA") components, to formulate a [set of semantic queries](https://github.com/TranslatorSRI/SRI_testing/blob/main/tests/onehop/README.md#how-the-testing-harness-works) against these components, validating the request inputs and response outputs of the queries for compliance to specified releases of the TRAPI specification and the Biolink Model (both defaulting to '_latest_').

The current implementation focuses on [unit testing of so-called 'one hop' queries of knowledge graph resources](https://github.com/TranslatorSRI/SRI_testing/blob/main/tests/onehop/README.md) using suitable permutations of the test data edge information into TRAPI **/query** endpoints of target components. 

## Specifying the Tests

For KP components, [JSON formatted specifications of input edge test data](https://github.com/TranslatorSRI/SRI_testing/blob/main/tests/onehop/README.md#kp-instructions) are accessed as internet-visible resources, the URL for which is recoded in a special Translator SmartAPI Registry ("Registry") extension property called **info.x-trapi.test_data_location**.  For a KP, posting such a KP test edge data configuration file as a REST accessible JSON file, then registering a SmartAPI registry entry with the required **info.x-trapi.test_data_location** pointing to the JSON file URL, is all that needs to be done to have the component tested by the system.

For ARA's, these queries are derived from ARA-associated KPs listed in their [ARA-specific JSON configuration file](https://github.com/TranslatorSRI/SRI_testing/blob/main/tests/onehop/README.md#ara-instructions), also dereferenced via a Registry **info.x-trapi.test_data_location** specified URL. As for the KP, posting such an ARA configuration file and setting the required **info.x-trapi.test_data_location** property in the ARA Registry entry, is all that is required to have the SRI Testing harness conduct the test.

## How it Works

The testing middleware leverages the [Pytest framework](https://docs.pytest.org/).  Essentially, the 'One Hops' PyTest script accesses Registry KP and ARA entries - which have their **info.x-trapi.test_data_location** properties set - to access the JSON test configuration data. Unit tests are then dynamically constructed as the cross-product of test edge data against semantic test types. These unit tests are then sequentially run then their output are captured as a hierarchical set of JSON documents which may be configured to be stored locally in the local filing system or within a Mongo database.

The back end validation of TRAPI message formats and Biolink Model compliance of message contents is mainly implemented in the complementary [Reasoner Validator](https://github.com/NCATSTranslator/reasoner-validator) package, which itself leverages the [Biolink Model Toolkit](https://github.com/biolink/biolink-model-toolkit) for Biolink Model validation.

A FastAPI web service API is coded which has endpoints to trigger a test run, monitor test run status and access the aforementioned hierarchical set of JSON test results.

The web service application (with its default FastAPI OpenAPI.json file structured web page) may be directly invoked from the command line, or accessed from a running Docker container specified by the local docker-compose.yaml (and associated Dockerfile) specifications. Once again, test results are also saved as static JSON documents either in the filing system or a Mongo database (depending on mode of site configuration), and upon test run completion, may be directly viewed(*) outside of the running instances of the web service and test scripts.

(*) Note that the default for command line running is file storage if a Mongo database server is not already running; for Docker container runs, a MongoDb database is set running and is used. For the latter, the Mongo-Express application may be used to view the data (the Docker Compose **mongodb-compose.yaml** specification file is provided to faciliate this) .
