---
title: Swap
parent: Memory
---

# Create swap file \(recommended vs. partition on SSD/flash for wear leveling\):  

```bash
fallocate -l 32G /swapfile  # Create file  
chmod 600 /swapfile  # Allow only root access  
mkswap /swapfile  # Designate as swap area  
swapon /swapfile  # Activate as swap  
```

If responds `swapon: /swapfile: swapon failed: Invalid argument`, filesystem may not support a swapfile.

## make permanent

Append to `/etc/fstab`: `/swapfile swap swap defaults 0 0`  

# Remove swap file:  

1. Deactivate swap: `sudo swapoff -v /swapfile`
1. remove entry from `/etc/fstab`
1. `sudo rm /swapfile`  

# Swap status:  

`swapon --show`  

`free -h`  
