---
title: Bootloaders & Booting
---

GRUB configuration:  
  Set in `/etc/default/grub`, then run `update-grub` to update `/boot/grub/grub.cfg`
 GRUB linux boot options  
  Select the appropriate boot entry \(Linux kernel\) in the GRUB menu  
  Press `e` to edit. Append option at the end of the kernel line  
   Options:  
    Boot to specific application, such as `/bin/bash`, rather than `init` / `systemd`:  
     `init=`
    Boot to target \(a.k.a. \):  
       
     Targets:  
      1: Single-User \(root only\).  
       Doesn't config network interfaces or start daemons.  
       \(exit via `ctrl-d` to continue booting to the default mode\)  
      2: Multi-User. Does not configure network interfaces or start daemons.  
      3: Multi-User with Networking. Starts the system normally.  
      5: X11. As 3 + display manager\(X\)  
  Press `ctrl-X` to boot  

 Bootloader: `extlinux` \(used on NVidia Jetson Nano\)  
  `/boot/extlinux/extlinux.conf`  
 Root boot argument  
  `/proc/cmdline`  


  Levels  
   0: Halt, 1: Single user, 2: Multi-user \(no networking\), 3: Multi-user \(networking\), 4: N/A, 5: Multi-user \(networking and GUI\), 6: Reboot  
  Check run level \(note: systemd uses targets\)  
   `sudo`  

 Shutdown:  
  `halt -p`  

 What's in our first program?  
 \(/sbin/init, unless changed in kernel parameter init=&lt;&gt;\)  
 If using Busybox, then reads `/etc/inittab`  
 If using System V, also reads `/etc/inittab`  
 Then look for initialization in `/etc/init.d`  
