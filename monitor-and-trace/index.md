---
title: Monitor & Trace
has_children: true
---

`sar`  
  can collect and display data over longer periods  
  Using `sar` utility you can do two things: 1\) Monitor system real time performance \(CPU, Memory, I/O, etc\) 2\) Collect performance data in the background on an on-going basis and do analysis on the historical data to identify bottlenecks.  

 Nagios: Monitor and notify on disk status, servers, services, etc.  
 uptime  
 both `w` and `uptime` command gets the information from the `/var/run/utmp` data file.
 (more good tools for debugging)

 `glances`
  an open source cross-platform monitoring tool. It provides tons of information on the small screen. It can also work in client/server mode.
 `strace` trace Linux system calls and signals  

 Linux system profiling tools / techniques  
  Look for book, such as [https://www.amazon.com/dp/1787283283/](https://www.amazon.com/dp/1787283283/)  

 Linux Event Notification  
  Write my own server? More flexible for functionality and protection  
  [https://www.binarytides.com/server-client-example-c-sockets-linux/](https://www.binarytides.com/server-client-example-c-sockets-linux/)  
   See fixes in comments  
  [http://www.tldp.org/LDP/LG/issue74/tougher.html](http://www.tldp.org/LDP/LG/issue74/tougher.html)  
  [http://www.linuxhowtos.org/C\_C++/socket.htm](http://www.linuxhowtos.org/C_C++/socket.htm)  
  [http://man7.org/linux/man-pages/man2/socket.2.html](http://man7.org/linux/man-pages/man2/socket.2.html)  
  [https://linux.die.net/man/7/socket](https://linux.die.net/man/7/socket)  
  For security, perhaps test system should be socket server and DUT should be client.  
   Client is enabled by a special command from test system, and will only then look for server.  

 Linux Health  
  [https://pcp.io/features.html](https://pcp.io/features.html)  
 Systems monitoring  
  [https://www.circonus.com/](https://www.circonus.com/) \(including embedded\)  
  [https://nodequery.com/](https://nodequery.com/)  
  [https://newrelic.com/](https://newrelic.com/)  
  [https://prometheus.io/](https://prometheus.io/)  
  [https://graphiteapp.org/](https://graphiteapp.org/)  
 IoT Device Dashboard and Visualization  
  [https://freeboard.io/](https://freeboard.io/) \(used by Ford for OpenXC Connected Car\)  
 Metrics and anomaly detection  
  [https://www.stathat.com/](https://www.stathat.com/)  
 API Monitoring  
  [https://www.runscope.com/](https://www.runscope.com/)  
 Performance monitoring  
  [https://blackfire.io/](https://blackfire.io/)  
 Load testing  
  [https://loader.io/](https://loader.io/)  
 Dashboard and logs  
  [https://www.datadoghq.com/](https://www.datadoghq.com/)  

 [https://www.tecmint.com/command-line-tools-to-monitor-linux-performance/](https://www.tecmint.com/command-line-tools-to-monitor-linux-performance/)  
  Monitorix is a free lightweight utility that is designed to run and monitor system and network resources as many as possible in Linux/Unix servers  
  Nmon CPU, Memory, Disk Usage, Network, Top processes, NFS, Kernel and much more  
  Collectl CPU usage, memory, network, inodes, processes, nfs, tcp, sockets and much more  

 `uptime` to check how long system has been running and how hard it’s working.  

Performance Co-Pilot:  
 Install   
  `yum install -y pcp, pcp-system-tools`  
 Take baseline of a metric \(kernel load\):  
   `pmval kernel.all.load`  
   for 10s:  
    `-T 10s`  
 Find the logger file directory:  
  `pcp | grep logger`  
 Show the logged kernel load \(replace with file spanning desired time\):  
  `pmrep -t 1m -a /20190519.03.03.0 kernel.all.load`

Security audit:
	sudo apt install wapiti
	wapiti -u https://jeffreyurban.com/ --scope folder
