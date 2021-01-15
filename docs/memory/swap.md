---
title: Swap
parent: Memory
---

Create swap file \(recommended vs. partition on SSD/flash for wear leveling\):  
  `sudo fallocate -l 32G /swapfile` \# Create file  
  `sudo chmod 600 /swapfile` \# Allow only root access  
  `sudo mkswap /swapfile` \# Designate as swap area  
  `sudo swapon /swapfile` \# Activate as swap  
  \(append to /etc/fstab to make permanent\)   
  If responds `swapon: /swapfile: swapon failed: Invalid argument`, filesystem may not support a swapfile.
  
  `/swapfile swap swap defaults 0 0`  
 Remove swap file:  
  `sudo swapoff -v /swapfile` \# Deactivate swap  
  \(remove entry from /etc/fstab\)  
  `sudo rm /swapfile`  
 Swap status:  
  `swapon --show`  
  `free -h`  
