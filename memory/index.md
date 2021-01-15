---
title: Memory
has_children: true
---

Available / in use:  
  `free -h`  
  `cat /proc/meminfo`  
 Virtual Memory  
  Repeat every 1 second:  
   `vmstat 1`  
 Swap:  
  Info:  
   `cat /proc/swaps`  
   `swapon -s`  
    Consider: swap is often disabled  
  Set partition to be swap:  
   `mkswap`   
  Swapiness:  
   General:  
    Low swappiness aids response for memory allocation  
    High swappiness is good with processes that sleep for a long time  
   Check:  
    `cat /proc/sys/vm/swappiness`  
   Change:  
    `sudo sysctl vm.swappiness=10`  
   Make permanent:  
    Edit file: `/etc/sysctl.conf`  
     Change or add: `vm.swappiness=10`  
    Reload: `sudo sysctl --load=/etc/sysctl.conf`  
 Kernel slab allocator:  
  `slabtop`  
 Virtual Memory Tuning:  
  General  
   See files in: `/proc/sys/vm`  
   Make permanent:  
    `/etc/sysctl.conf`  
  Writeback dirty memory by exceeding percentage of memory:  
   Percentage of dirty memory before flush to disk by `pdflush` background writeback daemon:  
    Check:  
     `sysctl vm.dirty_background_ratio`  
    Set:  
     `sysctl -w vm.dirty_background_ratio=`
   Percentage of dirty memory before flush to disk by user processes:  
    Check:  
     `sysctl vm.dirty_ratio`  
    Set:  
     `sysctl -w vm.dirty_ratio=`  
  Writeback dirty memory by exceeding age:  
   Interval to write back old data:  
    `dirty_writeback_interval`  
   Age threshold to write back old data:  
    `dirty_expire_interval`  
 Physical memory hardware specifications  
  Cache:  
   `dmidecode --type 7`  
  RAM:  
   `dmidecode --type 17`  

 Memory test:  
  `memtest` \(search package repo, with results such as memtest86+\)  

 `vmstat`  
  snapshot of current CPU, IO, processes, and memory usage, specify seconds for periodic  
  not the best for trending performance  

 `free`  
  memory statistics for both main memory and swap  
 `free` to check memory  

 Look at - debugs memory leak of running process, without recompiling or restarting  
  [https://github.com/WuBingzheng/memleax](https://github.com/WuBingzheng/memleax)  
  [https://linux.die.net/man/3/efence](https://linux.die.net/man/3/efence)  
  Purify  
   one more: I used `purify` a long time ago \(on solaris\) and it was a top-end tool, for its day. I think there is still a `purify` release for linux, but not sure if ARM is supported. \(purify was so good, that people would buy Sun boxes and port their C code over to solaris JUST to get the purify test results, even if x86 was their target.\)  
  [https://collectd.org/](https://collectd.org/)  
