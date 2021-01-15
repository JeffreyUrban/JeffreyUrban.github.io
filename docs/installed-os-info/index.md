---
title: Installed OS Info
---

Linux installation and host info:  
  `/etc/\*-release`  
  `hostnamectl`  

 Operating System identification data:  
  `/etc/os-release`  

 Check Operating System Identification data, including distribution  
  \(change existing entry\)  
   Operating System identification data:  
    `/etc/os-release`  
  \(to new entry\)  
   `cat /etc/_-release` \# includes redhat-release, os-release, etc.  

 Use `hostnamectl`, `cat /etc/*-release` to learn about our Linux installation and host configuration.

## To Organize

Distribution-Specific information: `lsb_release -dc`

Distribution-specific information:
	`lsb_release -a`
