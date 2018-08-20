## Monitoring Template

This is a docker-compose template for a collection of monitoring tools.

### Getting started

`docker-compose up`

If you are using OS X or Windows, ensure that you have allocated enough memory to the Docker process. Elasticsearch uses a lot of memory so at least 4GB is recommended.

### Centralised logging

To monitor and analyse application logs, the [ELK](https://www.elastic.co/products/stack) (Elasticsearch, Logstash, Kibana) stack is included.

#### Collecting log entries

By default, the Logstash pipeline is configured to accept log file entries from [Beats](https://www.elastic.co/products/beats) log shippers on port 5044. See the Filebeat [documentation](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-getting-started.html) for more details on how to configure a Beats log shipper.

It will also accept JSON log entries via TCP on port 5400. Example clients for JVM applications include:

* [logstash-logback-encoder](https://github.com/logstash/logstash-logback-encoder#tcp-appenders) - to send log entries via TCP in applications which make use of [Logback](https://logback.qos.ch)
* [log4j2 JSON layout](https://logging.apache.org/log4j/2.x/manual/layouts.html#JSONLayout) - the log4j2 JSON layout can be used along with a [SocketAppender](https://logging.apache.org/log4j/2.x/manual/appenders.html#SocketAppender) to send JSON events via TCP

### Distributed tracing

To collect and analyse application traces, [Zipkin](https://zipkin.io) is included. It is configured to use the Elasticsearch backend.

### Monitoring, metrics and alerting

To monitor application metrics and dispatch alerts, the [Prometheus](https://prometheus.io) monitoring and alerting toolkit is included.

#### Collecting metrics

To add a new Prometheus metrics target, edit the `./prometheus/prometheus.yml` file and add a new job. Prometheus also supports dynamically discovered targets based on a number of different discovery mechanisms. See the Prometheus [documentation](https://prometheus.io/docs/prometheus/latest/configuration/configuration/#<scrape_config>) for more details.

The [Prometheus Pushgateway](https://github.com/prometheus/pushgateway) is configured to accept metrics on port 9091. This can be used to push metrics from batch processes. Examples of using various different clients are available in the Prometheus [documentation](https://prometheus.io/docs/instrumenting/pushing/).

### Dashboards and Visualisation

To visualise metrics, [Grafana](http://grafana.com) is included.

It uses Prometheus as its datasource. Dashboards for Elasticsearch, Prometheus and Zipkin metrics are included out of the box.

Host metrics can also be collected by using the Prometheus [node_exporter](https://github.com/prometheus/node_exporter), but it is recommended to install and run this on the host directly.

#### Adding new dashboards

Dashboards are provisioned from the `./grafana/dashboards/` directory. To ensure that new dashboards are provisioned on startup simply export them to JSON from the Grafana UI and save them in this directory.
