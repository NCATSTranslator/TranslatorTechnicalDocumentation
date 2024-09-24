# Monitoring

Ensuring the health and performance of the Translator system will require the application of various strategies, for example:

* Endpoint uptime monitoring
* Telemetry from system components

# Endpoint uptime monitoring

Uptime monitoring can easily be turned on for Translator applications, using [UptimeRobot](https://uptimerobot.com/). Uptime and outage events can be reported directly to Translator Slack channels.

Contact Kevin Schaper for more information or to add new applications to monitor.

# Telemetry

Given the distributed nature of Biomedical Translator knowledge processing components, tracing the flow of queries through the system represents a challenge. Observability is the practice of measuring the state of a system by its various component outputs. [OpenTelemetry](https://opentelemetry.io/) is an open-source observability framework. Applying elements of OpenTelemetry to Translator helps with query auditing, quality assurance, and performance analysis.  

The [documentation](https://opentelemetry.io/docs/what-is-opentelemetry/) provided by OpenTelemetry is the best place to learn the basics. An OpenTelemetry system is composed of at least two parts: a client that exports telemetry data and a backend that collects telemetry data. Translator teams should implement the client side (exporters) in their applications, but not necessarily a backend.

Currently, Translator telemetry tools only support [traces](https://opentelemetry.io/docs/concepts/signals/traces/), not metrics or logs.

### Telemetry Instrumentation and Protocols

Translator components should [instrument](https://opentelemetry.io/docs/concepts/instrumentation/) their applications with a library that supports sending traces with the OpenTelemetry Protocol ([OTLP](https://opentelemetry.io/docs/specs/otel/protocol/)).

For most applications, libraries are available that will automatically instrument your application, without manually implementing anything specific. This will usually be enough for Translator purposes. For example, you should not need to manually handle associating spans and traces with their parents. However, if you would like to customize the information collected, and make your trace information more useful, you may want to add [baggage](https://opentelemetry.io/docs/concepts/signals/baggage/) to traces.

OTLP telemetry data can be sent over HTTP or gRPC. Both are supported by the Translator OpenTelemetry backend.

Previously, Translator applications were instrumented using [Jaeger Client Libraries](https://www.jaegertracing.io/docs/1.61/client-libraries/), utilizing the Thrift protocol, but these libraries have been deprecated, in favor of OTLP.

### Translator Deployment

Translator tools should send telemetry data to shared backend applications deployed on ITRB servers. The backend applications are implemented using [Jaeger](https://www.jaegertracing.io/). In the ITRB Kubernetes cluster, each maturity level has its own instance of Jaeger deployed, so that telemetry data from all the applications in any given maturity level is aggregated in one place, but not mixed across maturities. This also allows us to configure OTEL clients to send data to a consistent host endpoint across maturity levels.

Translator applications (clients) should configure their kubernetes deployments to send telemetry data to one of the following, and it should work for CI, test, and prod.

HTTP
jaeger-otel-collector:4318

gRPC
jaeger-otel-collector:4317

To view telemetry data, the Jaeger UI can be accessed with the following links: 
* [CI Jaeger](https://translator-otel.ci.transltr.io/search)
* [Test Jaeger](https://translator-otel.test.transltr.io/search)
* [Prod Jaeger](https://translator-otel.transltr.io/search)

### Examples

A simple demonstration of an OpenTelemetry implementation for python FastAPI servers is provided [here](https://github.com/TranslatorSRI/Jaeger-demo).

OpenTelemetry also provides a demo application [here](https://opentelemetry.io/docs/demo/).

Slides from the first Translator Relay session on OpenTelemetry can be found [here](https://docs.google.com/presentation/d/1OjcE1gVhx8u9EvvHGn6h50otBKmpd-9HidlTNppXXy0/edit#slide=id.g27ee40efb83_0_3).


### Telemetry Frequently Asked Questions
#### When I instrument my application should I trace incoming requests or outgoing?
In a microservices environment such as the Translator system, tracing both incoming and outgoing requests is key. Incoming tracing reveals user journeys, while outgoing tracing uncovers dependencies between services—both are crucial for comprehensive visibility and issue diagnosis.

As an example, ARAGORN, an ARA that receives requests from the ARS and performs subsequent requests to downstream components makes use of FastAPI instrumentation to trace incoming requests and httpx instrumentation for tracing outgoing requests. This [code snippet](https://github.com/ranking-agent/aragorn/blob/main/src/otel_config.py) shows how ARAGORN traces both incoming and outgoing requests.

#### When tracing outgoing requests, should calls to external services outside of Translator components be included?
Recording outgoing requests to external services can be essential for capturing communication details, aiding in troubleshooting, performance monitoring, and understanding dependencies outside your system.

#### In a Development environment with no provisioned Jaeger instance, what is the best way to test my OTEL implementation?

To use a local Jaeger instance for testing your OpenTelemetry implementation, you can follow these general steps:

1. **Install Jaeger:** Download and install Jaeger locally. You can use Docker to quickly set up a [Jaeger all-in-one](https://www.jaegertracing.io/docs/1.61/getting-started/#all-in-one) instance:
   ```bash
      docker run -d --name jaeger -p 16686:16686 -p 4317:4317 -p 4318:4318 jaegertracing/all-in-one:latest
   ```
   This command pulls the latest Jaeger image and runs it, exposing the Jaeger UI on port 16686.
2. **Configure OpenTelemetry SDK:** Use the OpenTelemetry SDK in your application to send traces to your local Jaeger instance. Configure your OpenTelemetry instrumentation to send data to localhost on the relevant Jaeger ports (4318 for HTTP and 4317 for gRPC).

3. **Instrument Your Code:** Instrument your application using OpenTelemetry APIs to create traces. Please make sure you've set up the instrumentation to export traces to your local Jaeger instance.

4. **Verify Traces:** Execute your application's workflows or requests that should generate traces. Then, access the Jaeger UI at http://localhost:16686 in your browser to view the traces generated by your application.


Remember to adapt the OpenTelemetry SDK configuration in your code to use the address and ports where your local Jaeger instance is running.

This approach provides a local environment for testing OpenTelemetry traces with Jaeger without needing a remote Jaeger instance.
