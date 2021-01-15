---
title: Logs
---

Kernel ring buffer  
  `dmesg -H` # Human readable  
 Journal  
  `/run`  
  `journalctl`  
  Specific boots:  
   Activate storage through reboot:  
    `/etc/systemd/journald.conf`
```
     [Journal]  
     Storage=persistent  
```
   List boots:  
    `journalctl --list-boots`  
   Filter by boot:  
    `journalctl -b`   
  Filter to specific unit:  
   `journalctl -u`   
 Syslog  
  `/var/log/syslog`  
 Log to `syslog` from command-line:  
  Message:  
   `logger`   
  Command output:  
   `logger $(command)`  
  File content:  
   `logger -f`   
  Options:  
   Limit size of entry \(truncates tokens, splits between lines on whitespace\):  
    `--size`   
   Suppress blank lines:  
    `-e`  
 Remote logging:  
  `/etc/rsyslog.conf`  # on client and server  
 Kernel crashdump  
  Enable:  
   `systemctl enable kdump && systemctl start kdump`  
  Dumps to:  
   `/var/kdump`  

 [https://www.digitalocean.com/community/tutorials/how-to-use-the-linux-auditing-system-on-centos-7](https://www.digitalocean.com/community/tutorials/how-to-use-the-linux-auditing-system-on-centos-7)  
 [https://linux-audit.com/tuning-auditd-high-performance-linux-auditing/](https://linux-audit.com/tuning-auditd-high-performance-linux-auditing/)  
  \*'Linux Auditing System', although may be too much overhead: see daemon auditd, /etc/audit/auditd.conf  
   e.g. `/var/log/audit/audit.log`  

 Data mining logs  
  Good info referenced here: [https://stackoverflow.com/questions/12129449/machine-learning-on-server-log-data](https://stackoverflow.com/questions/12129449/machine-learning-on-server-log-data)  
  [https://wand.net.nz/sites/default/files/Proposal\_0.pdf](https://wand.net.nz/sites/default/files/Proposal_0.pdf)  
  [https://www.infoworld.com/article/2608064/big-data/big-data-log-analysis-thrives-on-machine-learning.html](https://www.infoworld.com/article/2608064/big-data/big-data-log-analysis-thrives-on-machine-learning.html)  
  [https://stackoverflow.com/questions/22685261/anomaly-detection-on-syslog](https://stackoverflow.com/questions/22685261/anomaly-detection-on-syslog)  
  Splunk started its life as a log analysis system  
  [https://www.infoworld.com/article/3125012/artificial-intelligence/splunk-adds-machine-learning-thats-both-easy-and-open.html](https://www.infoworld.com/article/3125012/artificial-intelligence/splunk-adds-machine-learning-thats-both-easy-and-open.html)  
  [https://www.splunk.com/](https://www.splunk.com/)  
  Make syslog tool, but using fuzzy logic for more general state changes, things coming and going, esp. during extended operation.  
  Identify time sequence/offset relationships and look for them to be incomplete. Do A, expect B, C after delay.  
  Live journal filtering tool. Pipe in journal. Press keys to change filters.  

 Consider modifying `/etc/syslog-ng.conf` to deliver log entries in real time to diagnostic computer.  

 `syslog-ng` for parsing logs  

 Log parser elicitor  
  Iterative, interactive method. Work towards recursive definition.  
  Work backwards. Goal is category ID and meaningful JSON decomposition.  
   Hierarchical decomposition. Assign values to types.  

 Log entry ingestion and frequency / anomaly analysis  

 Syslog analysis from fleets  

 Syslog - Machine learning: Links look promising  
  [https://github.com/logpai/loglizer](https://github.com/logpai/loglizer)  
  [https://www.reddit.com/r/networking/comments/5lti8p/syslog\_data\_use\_in\_machine\_learning/](https://www.reddit.com/r/networking/comments/5lti8p/syslog_data_use_in_machine_learning/)  
  [https://unomaly.com/](https://unomaly.com/)  
  [https://stackoverflow.com/questions/22685261/anomaly-detection-on-syslog](https://stackoverflow.com/questions/22685261/anomaly-detection-on-syslog)  
  [https://logz.io/blog/machine-learning-log-analytics/](https://logz.io/blog/machine-learning-log-analytics/)  
  [https://www.upwork.com/hiring/for-clients/log-analytics-deep-learning-machine-learning/](https://www.upwork.com/hiring/for-clients/log-analytics-deep-learning-machine-learning/)  
  [https://www.ntt-review.jp/archive/ntttechnical.php?contents=ntr201311fa4.html](https://www.ntt-review.jp/archive/ntttechnical.php?contents=ntr201311fa4.html)  
  [https://www.networkworld.com/article/3256013/lan-wan/ai-machine-learning-and-your-access-network.html](https://www.networkworld.com/article/3256013/lan-wan/ai-machine-learning-and-your-access-network.html)  

 Real-time visualization, event detection, metrics from logs  
  Looks interesting - time series capture and live graphing  
   [https://graphiteapp.org/](https://graphiteapp.org/)  
   [https://www.loomsystems.com/blog/single-post/2017/06/07/prometheus-vs-grafana-vs-graphite-a-feature-comparison](https://www.loomsystems.com/blog/single-post/2017/06/07/prometheus-vs-grafana-vs-graphite-a-feature-comparison)  
    In the real world, Graphite is used in combination with Grafana; Graphite does the data storage, while Grafana does the visualization.  
  Look interesting - analyze logs  
   [https://goaccess.io/](https://goaccess.io/)  
   [https://help.sumologic.com/01Start-Here](https://help.sumologic.com/01Start-Here)  
   [https://logdna.com/](https://logdna.com/)  

 Inspect logs at /var/log. `zcat` for compressed log. `dmesg -h` for human readable.  

 JournalCtl  
  [https://www.digitalocean.com/community/tutorials/how-to-use-journalctl-to-view-and-manipulate-systemd-logs](https://www.digitalocean.com/community/tutorials/how-to-use-journalctl-to-view-and-manipulate-systemd-logs)  
  [https://blog.tjll.net/systemd-for-impatient-sysadmins/](https://blog.tjll.net/systemd-for-impatient-sysadmins/)  

 `journalctl`: Query system journal  
  `-f` to watch  
  `-u`  to filter  

Hardware issues - record in log:  
 `mcelog` \(daemon, Machine Check Exception\)  
