---
title: Copy, diff & Patch
grand_parent: Storage
parent: Files & Filesystems
---

 Duplicate disk \(such as SD Card\)  
  Duplicate entire disk, including partition table:  
   `sudo fdisk -l` \# Confirm without, with card to ensure correct device  
   `sudo dd if=/dev/ of=~/sd-card.img bs=4M status=progress` \# Set large block size to avoid slow read/write  
   Caution: Will erase complete target disk \(no need to format disk\)  
   `sudo dd if=~/sd-card.img of=/dev/ bs=4M status=progress`  
  Duplicate partition contents \(such as copying to larger SD Card to have more space\):  
   `sudo fdisk -l` \# Confirm desired partition within device  
   `sudo dd if=/dev/ of=~/partition.bin bs=4M status=progress` \# Set large block size to avoid slow read/write  
   \(ensure target partition is formatted to desired size\)  
   `sudo dd if=~/partition.bin of=/dev/partition status=progress`  

 Copy data  
  `dd if= of=file bs= count= seek=`  
