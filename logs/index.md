---
title: Logs
---

Inspect logs at /var/log. `zcat` for compressed log. `dmesg -h` for human readable.

# Kernel ring buffer  

`dmesg -H` _Human readable_

# Journal  

Query system journal  

`journalctl`  
- `-f` to watch  
- `-u`  to filter

[Tutorial](https://www.digitalocean.com/community/tutorials/how-to-use-journalctl-to-view-and-manipulate-systemd-logs)  

## Specific boots:  

Activate storage through reboot

`/etc/systemd/journald.conf`:

```
[Journal]  
Storage=persistent  
```

### List boots:  

`journalctl --list-boots`  

### Filter by boot:  

`journalctl -b`   

## Filter to specific unit:  

`journalctl -u`   

# Syslog  

`/var/log/syslog`  

## Log to `syslog` from command-line

### Message:  

`logger`   

### Command output:  

`logger $(command)`  

### File content:  

`logger -f`   

Options:  

- `--size`: Limit size of entry \(truncates tokens, splits between lines on whitespace\):  
- `-e`: Suppress blank lines:  

## Remote logging:  

`/etc/rsyslog.conf` _on client and server_

# Kernel crashdump  

Enable:  

`systemctl enable kdump && systemctl start kdump`  

Dumps to:  

`/var/kdump`  

# Linux auditing system

daemon `auditd`, `/etc/audit/auditd.conf`, `/var/log/audit/audit.log`

_Caution: may be too much overhead._

[Tutorial](https://www.digitalocean.com/community/tutorials/how-to-use-the-linux-auditing-system-on-centos-7)  

[Tuning](https://linux-audit.com/tuning-auditd-high-performance-linux-auditing/)  

# Data mining logs  

## Splunk 

Splunk started its life as a log analysis system  

## `syslog-ng` 

For parsing logs  

# `mcelog` Machine Check Exception

Hardware issues daemon

`mcelog`
