# Monitoring

Ensuring the health and performance of the Translator system will require the application of various strategies, for example:

* Endpoint uptime monitoring
* Telemetry from system components

# Endpoint uptime monitoring

T.B.A. (Tim Putnam to elaborate)

# Telemetry

Given the distributed nature of Biomedical Translator knowledge processing components, tracing the flow of queries through the system represents a challenge. Observability is the practice of measuring the state of a system by its various component outputs. [OpenTelemetry](https://opentelemetry.io/) is an open source observability framework. Applying elements of OpenTelemetry to Translator will help in the challenge of query auditing, for quality assurance or performance.  An overview of OpenTelemetry concepts is provided [here](https://docs.google.com/presentation/d/1OjcE1gVhx8u9EvvHGn6h50otBKmpd-9HidlTNppXXy0/edit#slide=id.g27ee40efb83_0_3) and a small Translator demo of the concept using the Jaeger telemetry collector, is [here](https://github.com/TranslatorSRI/Jaeger-demo).
