---
title: Bootloaders & Booting
---

# GRUB configuration
Set in `/etc/default/grub`, then run `update-grub` to update `/boot/grub/grub.cfg`

## GRUB linux boot options  
1. Select the appropriate boot entry (Linux kernel) in the GRUB menu  
1. Press `e` to edit. Append option at the end of the kernel line

    Options:  
    - Boot to specific application, such as `/bin/bash` (rather than `init` / `systemd`): `init=`
    - Boot to target (a.k.a.):  

        Targets:  
        - 1: Single-User \(root only\).
              Doesn't config network interfaces or start daemons.  
              _exit via `ctrl-d` to continue booting to the default mode_
        - 2: Multi-User. Does not configure network interfaces or start daemons.  
        - 3: Multi-User with Networking. Starts the system normally.  
        - 5: X11. As 3 + display manager\(X\)  
1. Press `ctrl-X` to boot  

# Bootloader: `extlinux` 
_used on NVidia Jetson Nano_  

Configuration: `boot/extlinux/extlinux.conf`  

Root boot argument: `/proc/cmdline`  

# Levels  
0. Halt
1. Single user
2. Multi-user (no networking)
3. Multi-user (networking)
4. N/A
5. Multi-user (networking and GUI)
6. Reboot  

Check run level: `runlevel`  
_Note: systemd uses targets, not runlevel_

Shutdown: `halt -p`  

# Post-boot scripts 
1. `/sbin/init`, unless changed in kernel parameter init=<>
1. If using Busybox or System V, then reads `/etc/inittab`  
1. Then look for initialization in `/etc/init.d`  
