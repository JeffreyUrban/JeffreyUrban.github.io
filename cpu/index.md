---
title: CPU
---

# per-process CPU utilization  

## `htop`  

Improved top. Better insight including short-lived processes.  

## `top` \(live, interactive\)  

### flags:  

Sorting: `-o %CPU`  

Run as highest priority (only as root, useful for overloaded system): `-q`  

### controls:  

- (up arrow, down arrow): Scroll  
- `<`, `>`: Select sort column  
- `f`: fields management  
- `c`: display absolute path for process  
- `z`: toggle color  
- Sorting  
  - `M`: memory usage  
  - `P`: CPU usage  
  - `N`: process ID  
  - `T`: running time  
  - `R`: reverse sort order
- `H`: toggle tasks / threads  
- `V`: toggle process parent-child view  
- `u`: select user  
- `o`: Add filter  
  - `COMMAND=`  
  - `!COMMAND=`  
  - `%MEM>1.0`
- `=:` Clear filters  
- `1`: Toggle CPU avg vs CPUs shown separately  

### tip:  

Add the 'DATA' field to show memory excluding shared resources which are included in VIRT, RES.  

### caution:  

Can miss short-lived processes  

## `pidstat`  

Similar to `top`, but outputs a stream.

## Profiling \(catches short-lived processes\):  

`sudo perf record -F 99 -ag -- sleep 10`  
`sudo perf report -nf --stdio`  

# CPU information  

`lscpu`  
`less /proc/cpuinfo`  
`nproc`  

# per-CPU utilization  

All processes, every second: `mpstat -P ALL 1`  

# CPU stats from PMC \(Performance Monitoring Counters: instructions per cycle, cache misses, etc\):  

`tiptop`  

# Service: `start`, `stop`, `restart`, `status`  

`sudo systemctl`

`sudo systemctl  {,}`  

# CPU core temp, frequency, utilization, power; Fan RPM; stress or monitor  

## s-tui

[Reference](https://github.com/amanusk/s-tui)  

`s-tui` 

select mode: Monitor / Stress  

 `mpstat` reports processors statistics  

 `mpstat -P ALL` monitor processors separately  

 `lscpu` to learn about processor(s)  

# Check performance \(of hashing\):  

`openssl speed`  

# Motherboard hardware information \(or Virtual Machine interface\):  

`dmidecode`  

# CPU temps

```
sudo apt install lm-sensors
sudo sensors-detect
sensors
```
