---
title: Elastic Stack
parent: Monitor & Trace
---

Most popular log analysis, spanning real-time visualization, event detection, metrics from logs.

Small-sized environment: beats -> (optionally for resiliency, add (Kafka, RabbitMQ, or Redis) -> logstash -> elasticsearch -> kibana  

If you need journaling, which is info on specific events or users, you have to use a log analyzer (like in ELK stack, not in Graphite + Graphana).

[Good Introduction](https://logz.io/learn/complete-guide-elk-stack/)

[Realtime analytics tutorial](https://dzone.com/articles/how-setup-realtime-alalytics)

# Beats 

Data collectors, for onboard monitoring of logs, events, metrics. Synchronizes when connected.

[Reference](https://www.elastic.co/guide/en/beats/libbeat/current/beats-reference.html)

[Community Beats](https://www.elastic.co/guide/en/beats/libbeat/current/community-beats.html)

Selected beats
- Filebeat: 
  - Logs. Handles log rotation transparently.  
- Heartbeat:
  - Pings / Host reachabilty. Ethernet and IP connections to other devices and endpoints  
- Metricbeat: 
  - CPU and process stats. CPU usage, memory, file system, disk IO, and network IO statistics, process CPU and memory  
- Packetbeat: 
  - IP traffic. Application latency and errors, response times, performance, access patterns.

# Logstash

Useful to pare down logged content.

[Reference](https://www.elastic.co/guide/en/logstash/current/index.html)

[Tutorial](https://logz.io/blog/logstash-tutorial/)

Logstash needs to be deployed with Redis to ensure reliability.

[Logstash Pitfalls](https://logz.io/blog/5-logstash-pitfalls-and-how-to-avoid-them/)

[Comparison with FluentD](https://logz.io/blog/fluentd-logstash/)

## Plugins

[Plugins Repo](https://github.com/logstash-plugins)

[A Guide to Logstash Plugins](https://logz.io/blog/logstash-plugins/)  

[Input Plugins](https://www.elastic.co/guide/en/logstash/current/input-plugins.html)
- Pull from existing syslog format log: [Syslog Input Plugin](https://www.elastic.co/guide/en/logstash/current/plugins-inputs-syslog.html)

[Filter Plugins](https://www.elastic.co/guide/en/logstash/current/filter-plugins.html)  
- Split structured text: [Dissect filter plugin](https://www.elastic.co/guide/en/logstash/current/plugins-filters-dissect.html)
- Mutations on fields: [Mutate Filter Plugin](https://www.elastic.co/guide/en/logstash/current/plugins-filters-mutate.html)
- Create events for each entry in a list field: [Split Filter Plugin](https://www.elastic.co/guide/en/logstash/master/plugins-filters-split.html)

[Output Plugins](https://www.elastic.co/guide/en/logstash/current/output-plugins.html)

[Codec Plugins](https://www.elastic.co/guide/en/logstash/current/codec-plugins.html)

[Contributing Plugins](https://www.elastic.co/guide/en/logstash/current/contributing-to-logstash.html)

## Scenarios 

[Tips for Linux Auth Logs](https://www.elastic.co/blog/grokking-the-linux-authorization-logs)

Extract structured fields from human-targeted logs: [Grok Processor](https://www.elastic.co/guide/en/elasticsearch/reference/master/grok-processor.html)

[Challenges with syslog](https://www.kartar.net/2014/09/when-logstash-and-syslog-go-wrong/)

[Machine learning for security analysis](https://www.elastic.co/blog/using-machine-learning-and-elasticsearch-for-security-analytics-deep-dive)

[App Search - Include Elastic Search in an App](https://www.elastic.co/blog/elastic-app-search-is-now-generally-available)

### Import / Export 

[Elasticsearch bulk import / export](https://github.com/skratchdot/elasticsearch-tools)
- Useful for test suites

[Elasticsearch Dump](https://github.com/taskrabbit/elasticsearch-dump)

[Snapshot and Restore](https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-snapshots.html)
