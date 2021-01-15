---
title: Intrusion Detection & Prevention System
parent: Network
---

Detects and alerts on potential vulnerability exploits against system or infrastructure  
 IDS can be positioned:  
  In-line with traffic \(i.e. on router or switch\)  
  Alongside traffic using TAP or SPAN, which mirrors router / switch traffic to another Ethernet port  
 IDS / IPS infrastructure:  
  Foundation: Rule engine \(e.g. Snort\)  
   Typically run as a service, with policy for frequent rule updates.  
   Outputs binary files \(for efficiency to keep up with traffic\)  
  Rule Manager \(e.g. Pulled Pork\)  
   Keeps rules updated  
  Parser \(e.g. Barnyard2\)  
   Reads binary file output  
  GUI \(e.g Snorby\)  
   Web interface for IDS / IPS  
  ---  
  Often difficult to set up complete infrastructure  
   Lots of configuration  
   Often compiling components from source  
   Often thin documentation \(need to read multiple setup guides\)  
 Snort  
  Used as packet sniffer, packet logger, or Intrusion Prevention System \(with commercial subscription\)  
  Extensible via open source components  
  Snort basic setup as an IDS:  
   `yum install -y epel-release`  
   \(install `daq`, `snort` from snort.org, since not in distribution package managers\)  
    Read install notes. May need to create symlink for libdnet, or do other things.  
    Note: Daq allows live updates of rulesets  
   `wget  -O community.tgz`  
   `tar xvzf community.tgz`  
   `cp community-rules/* /etc/snort/rules/`  
   Configure: `/etc/snort/snort.conf`  
   Rules \(include or define in\):  
    `/etc/snort/rules/.rules` # local.rules, community.rules, etc.  
    Note: Use 'Pulled Pork' for automation of rule updates  
    ---  
    Rules can generate alerts, and/or take actions  
     `community.rules` include some IPS \(dropping of packets for identified issues\)  
   Validate Configuration:  
    `snort -T -c /etc/snort/snort.conf`  
   Start:  
    `systemctl start snortd`  
   Check alerts:  
    `/var/log/snort/alert`  
