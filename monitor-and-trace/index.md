---
title: Monitor & Trace
has_children: true
---

# `sar`  

Can collect and display data over longer periods.

Using `sar` utility you can do two things:
1. Monitor system real time performance (CPU, Memory, I/O, etc.)
1. Collect performance data in the background on an on-going basis and do analysis on the historical data to identify bottlenecks.  

# Nagios

Monitor and notify on disk status, servers, services, etc.  

# `glances`

An open source cross-platform monitoring tool. It provides tons of information on the small screen. It can also work in client/server mode.

# Linux Health  

[https://pcp.io/features.html](https://pcp.io/features.html)  

# Systems monitoring  

- [https://www.circonus.com/](https://www.circonus.com/) (including embedded)  
- [https://nodequery.com/](https://nodequery.com/)  
- [https://newrelic.com/](https://newrelic.com/)  
- [https://prometheus.io/](https://prometheus.io/)  
- [https://graphiteapp.org/](https://graphiteapp.org/)  

# IoT Device Dashboard and Visualization  

[https://freeboard.io/](https://freeboard.io/) \(used by Ford for OpenXC Connected Car\)  

# Metrics and anomaly detection  

[https://www.stathat.com/](https://www.stathat.com/)  

# API Monitoring  

[https://www.runscope.com/](https://www.runscope.com/)  

# Performance monitoring  

[https://blackfire.io/](https://blackfire.io/)  

[https://www.tecmint.com/command-line-tools-to-monitor-linux-performance/](https://www.tecmint.com/command-line-tools-to-monitor-linux-performance/)  

Monitorix
- A free lightweight utility that is designed to run and monitor system and network resources as many as possible in Linux/Unix servers  

Nmon 
- CPU, Memory, Disk Usage, Network, Top processes, NFS, Kernel and much more  

Collectl
- CPU usage, memory, network, inodes, processes, nfs, tcp, sockets and much more

`uptime` to check how long system has been running and how hard it’s working.
 - both `w` and `uptime` command gets the information from the `/var/run/utmp` data file.

# Load testing  

[https://loader.io/](https://loader.io/)  

# Dashboard and logs  

[https://www.datadoghq.com/](https://www.datadoghq.com/)  

# Performance Co-Pilot

## Install   

`yum install -y pcp, pcp-system-tools`  

## Take baseline of a metric \(kernel load\):  

`pmval kernel.all.load`  

for 10s: `-T 10s`  

## Find the logger file directory:  

`pcp | grep logger`  

## Show the logged kernel load \(replace with file spanning desired time\):  

`pmrep -t 1m -a /20190519.03.03.0 kernel.all.load`

# Security audit:

```bash
sudo apt install wapiti
wapiti -u https://jeffreyurban.com/ --scope folder
```
