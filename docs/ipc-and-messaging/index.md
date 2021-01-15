---
title: IPC & Messaging
has_children: true
---

Tips on named pipes  
  [https://www.linuxjournal.com/article/2156](https://www.linuxjournal.com/article/2156)  
  [https://www.networkworld.com/article/3251853/linux/why-use-named-pipes-on-linux.html](https://www.networkworld.com/article/3251853/linux/why-use-named-pipes-on-linux.html)  

 Monitor dbus for more insight into IPC  
  [https://linux.die.net/man/1/dbus-monitor](https://linux.die.net/man/1/dbus-monitor)  

ZeroMQ -> broadcast and point to point  

 Msg Broker  
  Apache Kafka  
  RabbitMQ  

Set up published streams that processes can connect to when needed  
  ZeroMQ -&gt; Works brokerless. Basically, is a wrapper around TCP.  
   ZeroMQ docs \(look for Publish-Subscribe\): [http://zguide.zeromq.org/page:all](http://zguide.zeromq.org/page:all)  
   Python publisher example: [http://zguide.zeromq.org/py:wuserver](http://zguide.zeromq.org/py:wuserver)  
   Python subscriber example: [http://zguide.zeromq.org/py:wuclient](http://zguide.zeromq.org/py:wuclient)  
   Create generic stdin publisher application  
  Redis -&gt; Worth learning  
   [https://redis.io/](https://redis.io/)  
  RabbitMQ -&gt; Requires broker  
  D-Bus -&gt; stuck on same system  
  /dev/fanout -&gt; Appears not to be used  
   [http://compgroups.net/comp.linux.development.system/-dev-fanout-a-one-to-many-multi/2869739](http://compgroups.net/comp.linux.development.system/-dev-fanout-a-one-to-many-multi/2869739)  
   [http://www.linuxtoys.org/fanout/fanout.html](http://www.linuxtoys.org/fanout/fanout.html)  
