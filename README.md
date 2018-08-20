### Monitoring Template

This is a docker-compose template for a collection of monitoring tools.

#### Centralised logging

To monitor and analyse application logs, the [ELK](https://www.elastic.co/products/stack) (Elasticsearch, Logstash, Kibana) stack is included.

#### Distributed tracing

To collect and analyse application traces, [Zipkin](https://zipkin.io) is included. It is configured to use the Elasticsearch backend.

#### Monitoring, metrics and alerting

To monitor application metrics and dispatch alerts, the [Prometheus](https://prometheus.io) monitoring and alerting toolkit is included.

#### Visualisation

To visualise these metrics, [Grafana](http://grafana.com) is included. It uses the Prometheus metrics as its datasource.
