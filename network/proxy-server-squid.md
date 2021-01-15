---
title: Proxy Server - Squid
parent: Network
---

Use cases:  
  Bypass restrictions, enforce restrictions, improve web performance via caching, prioritize / de-prioritize traffic to certain sites.  
  Implement traffic shaping \(enforcing lower bitrates\)  
    Such as an ISP allocating bandwidth among customers who pay for performance tiers \(Requires buffering. Alternative is policing which drops faster traffic.\)  
   Such as ISP customer subject to policing, keeping below drop threshold to maintain QoS.  
 For transparency to clients:  
  Configure gateway to use a proxy server, instead of configuring client applications.

See also: SSH - Dynamic Tunnel \(SOCKS5 Proxy\)

## Types

### Forward Proxy

Works on behalf of client to forward requests

Open Proxy: A forwarding proxy that hides the client IP.

Includes:

* Anonymous: Hides IP, but is recognizable as a proxy
* Distorting: Changes the client IP, but is recognizable as a proxy
* Elite: Looks like a client, but with it's own IP

### Reverse Proxy

Works on behalf of server to route requests from clients

## Set up proxy server
```
  systemctl enable squid && systemctl start squid  
  firewall-cmd --permanent --add-service squid  
  firewall-cmd --reload  
```
  \# Configuration at: `/etc/squid/squid.conf`  
   Note: Order matters for entries  
   Blacklist:  
    `acl  dstdomain . .`  
     \# `acl`: Access Control List  
    `http_access deny`   
   Whitelist:  
    `acl  dstdomain . .`  
    `http_access allow`   
    Comment this line:  
     \# `http_access allow localnet`  
   Delay Pool \(bandwidth limiting\):  
```
    acl  src   
    delay\_pools   
    delay\_class    
     \# When affecting multiple IPs or range, delay class must be 2 or 3.  
    delay\_access  allow   
    delay\_access  deny all \# What is this line for?  
    delay\_parameters  / / /  
     \# Network -1/-1 for no limit.  
```
   Caching Server:  
    Note: Best with robust, dedicated disk  
    Use cases: Speeding up updates for many servers  
    Configuration:  
     Caching specific content  
   Apply changes:  
    `systemctl restart squid`  
 Set up client to use proxy server  
  `export http\_proxy="http://:3128"`  
 Check usage:  
  `/var/log/squid/access.log`  
