<img width="1460" alt="image" src="https://github.com/user-attachments/assets/c676602e-b836-480b-8463-e950148b3942" /># Infrastructure-monitoring-with-OpenTelemetry-in-Elastic-Observability
we are exploring as how to use the OpenTelemetry (OTel) collector to capture core system metrics like cpu,memory,disk,network,processes etc from various sources such as linux vm, openstack vm, amazon EC2, Google Compute, and individual physical/virtual systems running Linux and export these metrics/log/tracing to the centrallized log location like elasticsearch in this case.

The **hostmetrics** receiver in OpenTelemetry collects system-level metrics such as CPU, memory, and disk usage from the host machine in OTel Schema.


 There is a processor called **ElasticInfraMetricsProcessor**, which utilizes the opentelemetry-lib to convert these metrics into a format that Elastic UIs understand.

 The processor then forwards these metrics to the **Elasticsearch** Exporter, now enhanced to support exporting metrics in ECS mode. 

 ECS: Elastic Common Schema (ECS)

You dont have to install the elastic agent or opentelemetry collector to the linux system, You can run the Elastic Distribution for OpenTelemetry Collector by running the Elastic-Agent binary downloaded for your OS and architecture. Just download the elastic agent for your system and then cd to the directory and then run command ./elastic-agent in the otel mode like below:

You can also validate using the below command :

./elastic-agent otel validate  --config otel-config.yml


 ./elastic-agent otel --config otel-config.yml




FOR APM:

we need to use the OTLP exporter. In **hostmetrics** receiver we collects system-level metrics such as CPU, memory, and disk usage from the host machine in OTel Schema. These metrics are sent to the OTLP Exporter, which forwards them to the APM Server endpoint. 

exporters:
  otlphttp:
    endpoint: <mis_endpoint>
    tls:
      insecure: false
    headers:
      Authorization: <api_key_>
  logging:
    verbosity: detailed
