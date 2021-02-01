---
title: Memory
has_children: true
---

# Available / in use

`free -h`  

`cat /proc/meminfo`  

# Virtual Memory  

Repeat every 1 second: `vmstat 1`  

# Swap

## Info:  

`cat /proc/swaps`  

`swapon -s`  

_Consider: swap is often disabled_

## Set partition to be swap

`mkswap`   

## Swapiness:  

Low swappiness aids response for memory allocation  

High swappiness is good with processes that sleep for a long time  

### Check

`cat /proc/sys/vm/swappiness`  

### Change

`sudo sysctl vm.swappiness=10`  

### Make permanent

1. Edit file: `/etc/sysctl.conf`  
    - Change or add: `vm.swappiness=10`
1. Reload: `sudo sysctl --load=/etc/sysctl.conf`  

# Kernel slab allocator

`slabtop`  

# Virtual Memory Tuning

See files in: `/proc/sys/vm`  

Make permanent: `/etc/sysctl.conf`  

## Writeback dirty memory by exceeding percentage of memory

### Percentage of dirty memory before flush to disk by `pdflush` background writeback daemon

Check: `sysctl vm.dirty_background_ratio`  

Set: `sysctl -w vm.dirty_background_ratio=`

### Percentage of dirty memory before flush to disk by user processes

Check: `sysctl vm.dirty_ratio`  

Set: `sysctl -w vm.dirty_ratio=`  

## Writeback dirty memory by exceeding age

Interval to write back old data: `dirty_writeback_interval`  

Age threshold to write back old data: `dirty_expire_interval`  

# Physical memory hardware specifications  

Cache: `dmidecode --type 7`  

RAM: `dmidecode --type 17`  

# Memory test

`memtest` 

_search package repo, with results such as `memtest86+`_

# `vmstat`  

snapshot of current CPU, IO, processes, and memory usage, specify seconds for periodic  

_not the best for trending performance_

# `free`  

memory statistics for both main memory and swap  

 `free` to check memory  

# Debug memory

Debug memory leak of running process: `libleak`

Detect overrun and access after free vs malloc(): [efence](https://linux.die.net/man/3/efence)

Purify

# System stats 

[collectd](https://collectd.org/) The system statistics collection daemon
