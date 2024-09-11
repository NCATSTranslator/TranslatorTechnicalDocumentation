[Back to Testing](index.md)
# SRI Testing Infrastructure

The SRI Testing Infrastructure includes all components dealing with the automated and manual testing of the Translator system.

## Testing Components
- [Translator Testing Model](https://github.com/TranslatorSRI/TranslatorTestingModel) - schema relating to test resource specifications
- [Tests Repository](https://github.com/NCATSTranslator/Tests) - contains all test assets/cases/suites
- [Test Harness](https://github.com/TranslatorSRI/TestHarness) - automates running of queries and test runners
- [Information Radiator](https://informationradiator.renci.org) - display test results
- [ARAX GUI](https://arax.ci.transltr.io/?systest=1) - display test results
- [#translator-testing-alerts](https://app.slack.com/client/TSCGQ3XGB/C06G3EKKE8G) - Slack messages
- [Feedback Repo](https://github.com/NCATSTranslator/Feedback) - Translator issue reports
### Test Runners
- [Pass/Fail Test Runner](https://github.com/NCATSTranslator/ARS_Test_Runner) - Quality Assurance Testing
- [TRAPI Validation Test Runner](https://github.com/TranslatorSRI/graph-validation-test-runners) - System Level Testing
- [Benchmarks Test Runner](https://github.com/TranslatorSRI/Benchmarks) - Quality Assurance Testing
- (Coming Soon) [Performance Test Runner]() - Quality Assurance Testing

## Automated Pipeline
- A CronJob spins up a Docker Image of the Test Harness
- Test Harness downloads the Tests Repo and grabs the specified "Test Suite" based on the CronJob command
- Test Harness posts to Slack and creates a "Test Run" in the Information Radiator
- Test Harness loops over all of the "Test Cases" in the Test Suite
- For each Test Case, the Test Harness generates a TRAPI query, sends it to the System, and then passes along the responses
  - Test Harness then loops over the "Test Assets" within the Test Case
    - Test Harness creates a single "Test" in the Information Radiator
      - Based on the Test Case metadata, the Test Harness passes the Test Asset and query responses along to a "Test Runner"
      - Test Runner performs its specific type of evaluation (pass/fail, TRAPI validation, MCQ, Pathfinder, etc.) and returns a test report
      - Test Harness uploads the test result to Information Radiator
- Once all tests have been run, the Test Harness posts to Slack with the results, sets the Test Run to complete in the Information Radiator, and the ARAX GUI then retrieves the results from the Information Radiator for display there

## Manual Testing
Manual Tests are largely done by Translator consortium members who manually query the System and then evaluate the results they see.
If issues are found, a GitHub Issue is then created in the [Feedback Repo](https://github.com/NCATSTranslator/Feedback).
Those issues are then triaged and assigned to the relevent/offending developer teams.
