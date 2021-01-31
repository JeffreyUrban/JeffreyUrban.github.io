---
title: Kernel
---

# System calls

## Strace

`strace -p`   

Use with EXTREME caution:  
- Can slow process dramatically, i.e. 1/100x  
- Can cause an application to hang on exit  

## sysdig

 `sysdig proc.name=`  

# Interrupts 

`cat /proc/interrupts`  

- Each line represents an installed handler  
- 1st column is interrupt number 
- Columns 2+ are per-CPU count since boot
- Last column is handler and device

# Modules

## Built-in:  

`cat /lib/modules/$(uname -r)/modules.builtin`  

## Currently loaded:  

`lsmod`  

## All available modules:  

`find /lib/modules/$(uname -r)/ -type f -name .ko`  

_Module name does not include extension_

## Module info \(including available parameters\):  

`modinfo`   

## Basic utilities \(Avoid. Better to use `modprobe`\)  

### Load module:  

`insmod .ko`  

### Remove module:  

`rmmod`   

## Advanced utility `modprobe` \(dependency resolution, error checking, etc\)  

### Load module:  

`modprobe`   

(with parameter): `modprobe  =`  

### Remove module:  

`modprobe -r`   

_Removes unused dependencies as well_

## Update dependency information for new modules:  

`depmod -A`  

## Check parameters as loaded:  

### For one module:  

`cat /sys/module//parameters/`  

### For all modules:  

`sysctl -a`  

## Change parameter of loaded module:  

### Non-persistent  

`sysctl -w <.-delimited module parameter name>=`  

### Persistent  

`echo "options  =" > /etc/modprobe.d/.conf`  

`/etc/sysctl.conf`  

`/etc/modules-load.d`  

# SysRq (System Request)

## General  

Key combinations to directly message kernel, useful on a dying system.  

'SysRq' is a special key (not present on Apple keyboards).  

## Turn on:  

`echo 1 > /proc/sys/kernel/sysrq`  

## Commands \(selected\):  

List options: `SysRq-h`  

Sync dirty buffers to disk: `SysRq-s`  

Unmount all filesystems: `SysRq-u`  

Reboot the machine: `SysRq-b`  

Dump memory information to console: `SysRq-m`  

# Update Ubuntu Linux kernel  

[Reference](https://www.wikihow.com/Update-Ubuntu-Kernel)  

# Linux kernel testing  

LTP, Linux test project (rec. by Maynard)  

[See also](https://github.com/gormanm/mmtests)  
