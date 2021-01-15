---
title: MQTT & mosquitto
parent: IPC & Messaging
has_children: true
---

Make a looping input that I can pipe into commands  
  [https://www.digitalocean.com/community/questions/how-to-setup-a-mosquitto-mqtt-server-and-receive-data-from-owntracks](https://www.digitalocean.com/community/questions/how-to-setup-a-mosquitto-mqtt-server-and-receive-data-from-owntracks)  
   mqtt:  
    rm mqtt; mkfifo mqtt; while \(true\); do cat  \| pv -l -L 10 -q &gt; mqtt; done  
    sudo mosquitto -c /etc/mosquitto/mosquitto.conf  
    cat &lt; mqtt \|   

 MQTT topics minimal hash  
  String compare each to check for uncatalogued topics  
  Look at mosquitto client: [https://github.com/eclipse/mosquitto/tree/a9da3c263d315b14a7f5aa2e0e62de760e8e2c3d/client](https://github.com/eclipse/mosquitto/tree/a9da3c263d315b14a7f5aa2e0e62de760e8e2c3d/client)  

 For mqtt topics instead of loop string compare consider:  
  Minimal hash \(faster\)  
  Trie on subtopics \(less risk to change or error\)  

 Set up a mosquitto broker with username and password:  
  [https://www.vultr.com/docs/how-to-install-mosquitto-mqtt-broker-server-on-ubuntu-16-04](https://www.vultr.com/docs/how-to-install-mosquitto-mqtt-broker-server-on-ubuntu-16-04)  

 Start server \(or enable via systemd\):  
  mosquitto -d  

 [https://github.com/eclipse/paho.mqtt-spy](https://github.com/eclipse/paho.mqtt-spy)  
