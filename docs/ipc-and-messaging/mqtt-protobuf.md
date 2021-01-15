---
title: MQTT / Protobuf
parent: MQTT & mosquitto
grand_parent: IPC & Messaging
---

MQTT/ Protobuf  
  MQTT + protobuf  
   protobuf: [http://tleyden.github.io/blog/2014/12/02/getting-started-with-go-and-protocol-buffers/](http://tleyden.github.io/blog/2014/12/02/getting-started-with-go-and-protocol-buffers/)  
   MQTT: [https://www.eclipse.org/paho/clients/golang/](https://www.eclipse.org/paho/clients/golang/)  
  Kafka + MQTT + protobuf + Live UI  
   [https://kafka.apache.org/quickstart](https://kafka.apache.org/quickstart)  
   [https://docs.confluent.io/current/installation/installing\_cp/deb-ubuntu.html](https://docs.confluent.io/current/installation/installing_cp/deb-ubuntu.html)  
   [https://docs.confluent.io/current/installation/installing\_cp/dev-cli.html\#installing-cp](https://docs.confluent.io/current/installation/installing_cp/dev-cli.html#installing-cp)  
   [https://github.com/kaiwaehner/kafka-connect-iot-mqtt-connector-example/blob/master/live-demo-kafka-connect-iot-mqtt-connector.adoc\#change-log-level-of-kafka-connect](https://github.com/kaiwaehner/kafka-connect-iot-mqtt-connector-example/blob/master/live-demo-kafka-connect-iot-mqtt-connector.adoc#change-log-level-of-kafka-connect)  
   install connectors  
```
    sudo confluent-hub install confluentinc/kafka-connect-mqtt:latest  
    sudo confluent-hub install blueapron/kafka-connect-protobuf-converter:latest  
```
   Create file mqtt.properties. cat mqtt.properties  
```
    name=mqtt-source  
    tasks.max=1  
    connector.class=io.confluent.connect.mqtt.MqttSourceConnector  
    mqtt.server.uri=tcp://:1883  
    mqtt.topics=  
    kafka.topics=mqtt.  
```
   Steps to connect to MQTT:  
```
    confluent start connect  
    confluent load mqtt-source -d mqtt.properties  
```
  …  
    \(when done\)  
    `confluent destroy`  
   Steps to consume from Kafka  
    `kafka-console-consumer --bootstrap-server localhost:9092 --topic mqtt. --property print.key=true --from-beginning`  
   [https://github.com/kaiwaehner/ksql-fork-with-deep-learning-function](https://github.com/kaiwaehner/ksql-fork-with-deep-learning-function)  
  Kafka + Protobuf \(convert on the way out for now\)  
   [https://www.confluent.io/connector/kafka-connect-protobuf-converter/](https://www.confluent.io/connector/kafka-connect-protobuf-converter/)  
   [https://github.com/blueapron/kafka-connect-protobuf-converter](https://github.com/blueapron/kafka-connect-protobuf-converter)  
  Kafka + KSQL  
   [https://github.com/kaiwaehner/ksql-fork-with-deep-learning-function](https://github.com/kaiwaehner/ksql-fork-with-deep-learning-function)  
  Kafka + MQTT  
   [https://www.confluent.io/connector/kafka-connect-mqtt/](https://www.confluent.io/connector/kafka-connect-mqtt/)  
    [https://docs.confluent.io/current/connect/kafka-connect-mqtt/mqtt-sink-connector/index.html](https://docs.confluent.io/current/connect/kafka-connect-mqtt/mqtt-sink-connector/index.html)  
   [https://thenewstack.io/apache-kafka-cornerstone-iot-data-platform/](https://thenewstack.io/apache-kafka-cornerstone-iot-data-platform/)  
   [https://dzone.com/articles/apache-kafka-mqtt-end-to-end-iot-integration-githu](https://dzone.com/articles/apache-kafka-mqtt-end-to-end-iot-integration-githu)  
   [https://dzone.com/articles/mqtt-apache-kafka-influxdb-sql-iot-harmony](https://dzone.com/articles/mqtt-apache-kafka-influxdb-sql-iot-harmony)  
   [https://kafka-summit.org/sessions/processing-iot-data-end-end-mqtt-apache-kafka/](https://kafka-summit.org/sessions/processing-iot-data-end-end-mqtt-apache-kafka/)  
   [http://www.kai-waehner.de/blog/2018/09/10/apache-kafka-mqtt-end-to-end-iot-integration-demo-scripts-github/](http://www.kai-waehner.de/blog/2018/09/10/apache-kafka-mqtt-end-to-end-iot-integration-demo-scripts-github/)  
  Protobuf Links to look at again  
   [https://protogen.marcgravell.com/decode](https://protogen.marcgravell.com/decode)  
   [https://mobilebit.wordpress.com/2013/09/25/protobuf-mqtt-yummy-fast/](https://mobilebit.wordpress.com/2013/09/25/protobuf-mqtt-yummy-fast/)  
   [https://github.com/mwielgoszewski/burp-protobuf-decoder](https://github.com/mwielgoszewski/burp-protobuf-decoder)  
   [https://www.farsightsecurity.com/2015/04/17/mschiffm-nmsg-protobuf-deserialize/](https://www.farsightsecurity.com/2015/04/17/mschiffm-nmsg-protobuf-deserialize/)  
   [https://blog.gopheracademy.com/advent-2017/make/](https://blog.gopheracademy.com/advent-2017/make/)  
   [https://medium.com/@at\_ishikawa/cli-to-generate-protocol-buffers-c2cfdf633dce](https://medium.com/@at_ishikawa/cli-to-generate-protocol-buffers-c2cfdf633dce)  
   [http://google.github.io/proto-lens/installing-protoc.html](http://google.github.io/proto-lens/installing-protoc.html)  
   [https://stackoverflow.com/questions/35049657/how-to-decode-binary-raw-google-protobuf-data](https://stackoverflow.com/questions/35049657/how-to-decode-binary-raw-google-protobuf-data)  
   [https://stackoverflow.com/questions/34952811/is-there-a-definitive-nix-command-line-tool-for-inspecting-protocol-buffers](https://stackoverflow.com/questions/34952811/is-there-a-definitive-nix-command-line-tool-for-inspecting-protocol-buffers)  
   [https://developers.google.com/protocol-buffers/docs/overview](https://developers.google.com/protocol-buffers/docs/overview)  
  Protobuf  
   [https://developers.google.com/protocol-buffers/](https://developers.google.com/protocol-buffers/)  
   This looks useful for working with them. See gRPC: [https://github.com/uber/prototool](https://github.com/uber/prototool)  
   See protoc --decode and --decode\_raw: [https://stackoverflow.com/questions/34952811/is-there-a-definitive-nix-command-line-tool-for-inspecting-protocol-buffers](https://stackoverflow.com/questions/34952811/is-there-a-definitive-nix-command-line-tool-for-inspecting-protocol-buffers)  
   May be useful for interpreting .proto files: [https://pypi.org/project/protobuf-tools/](https://pypi.org/project/protobuf-tools/)  
   Command-line example for decoding protobuf: [https://stackoverflow.com/questions/35049657/how-to-decode-binary-raw-google-protobuf-data](https://stackoverflow.com/questions/35049657/how-to-decode-binary-raw-google-protobuf-data)  
