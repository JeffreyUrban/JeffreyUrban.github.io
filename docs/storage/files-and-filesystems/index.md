---
title: Files & Filesystems
parent: Storage
has_children: true
---

 `lsof` open files  

 [https://www.logicmonitor.com/support/monitoring/os-virtualization/monitoring-remote-linux-files/](https://www.logicmonitor.com/support/monitoring/os-virtualization/monitoring-remote-linux-files/)  
  Generally, it is best practice to avoid remote execution for monitoring purposes, whenever possible. In most cases, it should be possible to serve the information that you would like to monitor via a webpage, API, SNMP, or database connection so that it can be accessed remotely from the collector machine with very little overhead.  

 Process `mmcqd`  
  `mmcqd` is related to defragmentation after moving a big file.  
 Troubleshoot and track EMMC performance: `mmc-util` / `mmc-utils`  

 Robust file systems to consider  
  `btrfs`, `jfs` \(from ibm\), `xfs` \(`sgi`\), `f2fs`  

 `fswatch` notifies on changed files  

 Secure erase with random and zero overwrite:  
  `shred -zvu`   

`fallocate` image file
	On my laptop, I can use `fallocate` to create a file. Let's say it's a 1G file. I have no control of where on the disk that file will be placed, but the new file will use up 1G of space from the unused space on the disk, just like any other new file. Although we created the file, `fallocate` does not initialize the file's contents, so if we try to read the contents, we should expect it to be full of random junk, which includes the remnants of old files we've deleted.
	Thus, the fallocated img file is similar to a random sd card that may have some random stuff on it already, except, unlike an sd card, it's basically impossible that the fallocated image would actually be usable as-found.
	You know when you format a disk, you can choose to initialize/wipe it and it takes a lot longer... that's writing zeros to the whole disk. But if you don't initialize, the format happens very quickly, because it just leaves all of the original junk in place on the disk, but you don't see it because it is not referenced anywhere by the partitions/filesystems.
	An image file that we create with `fallocate` is just an uninitialized file.

Resize file (such as image)
	`truncate`

