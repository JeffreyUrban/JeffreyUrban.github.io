---
title: MQTT & mosquitto
parent: IPC & Messaging
has_children: true
---

# Set up broker and client

[Set up a mosquitto broker with username and password](https://www.vultr.com/docs/how-to-install-mosquitto-mqtt-broker-server-on-ubuntu-16-04)

Start server (or enable via systemd):

`mosquitto -d`

[Mosquitto client](https://github.com/eclipse/mosquitto/tree/a9da3c263d315b14a7f5aa2e0e62de760e8e2c3d/client)

# Make a looping input that I can pipe into commands  

[Refernece](https://www.digitalocean.com/community/questions/how-to-setup-a-mosquitto-mqtt-server-and-receive-data-from-owntracks)  

```
rm mqtt; mkfifo mqtt
while (true)
    do cat | pv -l -L 10 -q > mqtt 
done  
sudo mosquitto -c /etc/mosquitto/mosquitto.conf  
cat < mqtt | ...  
```

# MQTT topics minimal hash  

String compare each to check for uncatalogued topics  

# MQTT topic filtering

Better options than loop string compare:
- Minimal hash (faster)  
- Trie on subtopics (less risk to change or error)
