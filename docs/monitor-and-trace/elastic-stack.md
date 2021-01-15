---
title: Elastic Stack
parent: Monitor & Trace
---

More on ELK  
  [https://www.elastic.co/guide/en/logstash/current/running-logstash-command-line.html](https://www.elastic.co/guide/en/logstash/current/running-logstash-command-line.html)  
  [https://www.elastic.co/guide/en/logstash/current/input-plugins.html](https://www.elastic.co/guide/en/logstash/current/input-plugins.html)  
  [https://www.elastic.co/guide/en/logstash/current/plugins-filters-dissect.html](https://www.elastic.co/guide/en/logstash/current/plugins-filters-dissect.html)  
  [https://www.elastic.co/guide/en/logstash/current/plugins-filters-mutate.html](https://www.elastic.co/guide/en/logstash/current/plugins-filters-mutate.html)  
  [https://www.elastic.co/guide/en/logstash/current/filter-plugins.html](https://www.elastic.co/guide/en/logstash/current/filter-plugins.html)  
  [https://www.elastic.co/guide/en/logstash/current/output-plugins.html](https://www.elastic.co/guide/en/logstash/current/output-plugins.html)  
  [https://www.elastic.co/guide/en/logstash/current/contributing-to-logstash.html](https://www.elastic.co/guide/en/logstash/current/contributing-to-logstash.html)  
  [https://logz.io/blog/5-logstash-pitfalls-and-how-to-avoid-them/](https://logz.io/blog/5-logstash-pitfalls-and-how-to-avoid-them/)  
  [https://logz.io/blog/logstash-plugins/](https://logz.io/blog/logstash-plugins/)  
  [https://discuss.elastic.co/t/parsing-a-json-array-of-objects/55441/5](https://discuss.elastic.co/t/parsing-a-json-array-of-objects/55441/5)  
  [https://www.elastic.co/guide/en/logstash/master/plugins-filters-split.html](https://www.elastic.co/guide/en/logstash/master/plugins-filters-split.html)  
 For syslog and other system logs  
  [https://www.elastic.co/guide/en/logstash/current/plugins-inputs-syslog.html](https://www.elastic.co/guide/en/logstash/current/plugins-inputs-syslog.html)  
  [https://www.elastic.co/blog/grokking-the-linux-authorization-logs](https://www.elastic.co/blog/grokking-the-linux-authorization-logs)  
  [https://www.elastic.co/guide/en/elasticsearch/reference/master/grok-processor.html](https://www.elastic.co/guide/en/elasticsearch/reference/master/grok-processor.html)  
  [https://www.elastic.co/guide/en/logstash/current/config-examples.html](https://www.elastic.co/guide/en/logstash/current/config-examples.html)  
  [https://www.kartar.net/2014/09/when-logstash-and-syslog-go-wrong/](https://www.kartar.net/2014/09/when-logstash-and-syslog-go-wrong/)  

 Investigate logstash reliability and consider implementing with Redis  
  [https://logz.io/blog/fluentd-logstash/](https://logz.io/blog/fluentd-logstash/)  
   Logstash: Needs to be deployed with Redis to ensure reliability  

 Real-time visualization, event detection, metrics from logs  
 ELK Stack - most popular log analysis  
  [https://logz.io/learn/complete-guide-elk-stack/](https://logz.io/learn/complete-guide-elk-stack/)  
   Has tutorial  
  [https://dzone.com/articles/how-setup-realtime-alalytics](https://dzone.com/articles/how-setup-realtime-alalytics)  
  [https://blog.takipi.com/production-tools-guide/visualization-and-metrics/](https://blog.takipi.com/production-tools-guide/visualization-and-metrics/)  
    If you need journaling, which is info on specific events or users, you have to use a log analyzer \(like in ELK stack, not in Graphite + Graphana\).  
  [https://www.elastic.co/products/kibana](https://www.elastic.co/products/kibana)  
  Small-sized environment: beats -&gt; \(optionally for resiliency, add \(Kafka, RabbitMQ, or Redis\) -&gt; logstash -&gt; elasticsearch -&gt; kibana  
  Logstash  
   [https://logz.io/blog/logstash-tutorial/](https://logz.io/blog/logstash-tutorial/)  
   [https://www.elastic.co/guide/en/logstash/current/first-event.html](https://www.elastic.co/guide/en/logstash/current/first-event.html)  
   [https://www.elastic.co/guide/en/logstash/6.4/dir-layout.html](https://www.elastic.co/guide/en/logstash/6.4/dir-layout.html)  
   [https://www.elastic.co/guide/en/logstash/current/advanced-pipeline.html](https://www.elastic.co/guide/en/logstash/current/advanced-pipeline.html)  

 [https://www.elastic.co/products/beats/metricbeat](https://www.elastic.co/products/beats/metricbeat)  

 Elasticsearch  
  [https://www.elastic.co/elasticon/2015/sf/unlocking-interplanetary-datasets-with-real-time-search](https://www.elastic.co/elasticon/2015/sf/unlocking-interplanetary-datasets-with-real-time-search)  

 Look into Kibana vega [https://www.elastic.co/guide/en/kibana/current/vega-graph.html](https://www.elastic.co/guide/en/kibana/current/vega-graph.html)  

 Look at filebeat system module.  
  [https://www.elastic.co/guide/en/beats/filebeat/6.5/filebeat-modules-quickstart.html](https://www.elastic.co/guide/en/beats/filebeat/6.5/filebeat-modules-quickstart.html)  

 Syslog - Machine learning: Links look promising  
  [https://www.elastic.co/blog/using-machine-learning-and-elasticsearch-for-security-analytics-deep-dive](https://www.elastic.co/blog/using-machine-learning-and-elasticsearch-for-security-analytics-deep-dive)  

 Filter log messages that designate state change  
  Such as network device state change  
  [https://www.elastic.co/guide/en/x-pack/current/how-watcher-works.html](https://www.elastic.co/guide/en/x-pack/current/how-watcher-works.html)  

 Look at Elasticsearch export and import for per-test-suite use  
  [https://github.com/skratchdot/elasticsearch-tools](https://github.com/skratchdot/elasticsearch-tools)  
  [https://github.com/taskrabbit/elasticsearch-dump](https://github.com/taskrabbit/elasticsearch-dump)  
  [https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-snapshots.html](https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-snapshots.html)  

 Elastic Stack  
  Explore metricbeat output first. Check visualizations, which can be combined into dashboards.  
  Logstash to pare down logged content  
  Logstash plugins \(including protobuf converter, trigger actions on inputs\)  
   [https://github.com/logstash-plugins](https://github.com/logstash-plugins)  
   [https://logz.io/blog/logstash-plugins/](https://logz.io/blog/logstash-plugins/)  
   [https://www.elastic.co/guide/en/logstash/current/input-plugins.html\#input-plugins](https://www.elastic.co/guide/en/logstash/current/input-plugins.html#input-plugins)  
   [https://www.elastic.co/guide/en/logstash/current/output-plugins.html](https://www.elastic.co/guide/en/logstash/current/output-plugins.html)  
   [https://www.elastic.co/guide/en/logstash/current/filter-plugins.html](https://www.elastic.co/guide/en/logstash/current/filter-plugins.html)  
   [https://www.elastic.co/guide/en/logstash/current/codec-plugins.html](https://www.elastic.co/guide/en/logstash/current/codec-plugins.html)  
  Try more features:  
   [https://www.elastic.co/products/stack](https://www.elastic.co/products/stack)  
  App Search is a means for elastic API for inclusion in an app  
   [https://www.elastic.co/blog/elastic-app-search-is-now-generally-available](https://www.elastic.co/blog/elastic-app-search-is-now-generally-available)  
  Check out more resources  
   [https://www.elastic.co/community](https://www.elastic.co/community)  
  Sign up for conference  
   [https://www.elastic.co/elasticon/tour/2019/san-francisco](https://www.elastic.co/elasticon/tour/2019/san-francisco)  
  Try more beats  
   [https://github.com/raboof/connbeat](https://github.com/raboof/connbeat)  
   [https://github.com/christiangalsterer/execbeat](https://github.com/christiangalsterer/execbeat)  
   [https://github.com/ctindel/fastcombeat](https://github.com/ctindel/fastcombeat)  
   [https://github.com/eskibars/lmsensorsbeat](https://github.com/eskibars/lmsensorsbeat)  
   [https://github.com/nathan-K-/mqttbeat](https://github.com/nathan-K-/mqttbeat)  
   [https://github.com/benben/serialbeat](https://github.com/benben/serialbeat)  
   [https://github.com/berfinsari/tracebeat](https://github.com/berfinsari/tracebeat)  

 elastic dashboard metric  
 elastic event notification \(Watcher\)  
  Watcher  
   Requires elasticsearch  
   May require license  
   May operate only on schedule, not immediately on event  
   Supports more complicated expressions  
  Compare to Python  
   Build into interface supervisor  
   Direct access to data on receipt. No delay.  

 Beats data collectors  
  Onboard monitoring of logs, events, metrics. Synchronizes with diagnostic computer when connected.  
  ----------  
  Filebeat: Logs. Handles log rotation transparently.  
  Heartbeat: Pings / Host reachabilty. Ethernet and IP connections to other devices and endpoints  
  Metricbeat: CPU and process stats. CPU usage, memory, file system, disk IO, and network IO statistics, process CPU and memory  
  Packetbeat: IP traffic. Application latency and errors, response times, performance, access patterns.  
