---
title: Processes
---

List:  
  For all users:  
   `ps aux` \# a:all-users, u:user-oriented display, x: including w/out control terminal  
   `ps lax` \# l:long-format, faster without u  
   `ps -e`  
   Other options:  
    `w`, `ww` \# extra columns, full width  
  Details with parent / child relationships:  
   `ps -ef f`  
  With real-time priority \(specified columns\):  
   `ps -eo state,uid,pid,ppid,rtprio,time,comm`  
  Threads:  
   `ps -AlFH`  
 Get ID\(s\):  
  `pgrep`   
  `pidof`   
 Time:  
  `pidstat`  
   `-t`: time, including user vs system %  
   `-d`: read/write rates and delay  
  `time`   
 Library calls:  
  `ltrace`   
 systemd service information  
   `sudo systemctl status`   
 Check / increase maximum number of PIDs:  
   `/proc/sys/kernel/pid_max`  
  Caution: Deviating from default 32,768 May break applications  
 Zombies:  
  List them:  
   `ps aux | grep -w defunct`  
  Remove them:  
   `kill -s SIGCHLD`   
 Daemons  
  Check all:  
   `systemctl status`  
  List all loaded & active services:  
   `systemctl --type=service`  
  Check dependencies:  
   `systemctl list-dependencies`  
  Reload daemons \(after fixing dependencies\):  
   `systemctl daemon-reload`  
 Memory map \(virtual memory ranges, permissions, linked libraries / shared segments / etc\):  
   `cat /proc//maps`  
   format: start-end, permission, offset, major:minor, inode, file  
  `pmap`   

 `ps -e` information about the running process  
 `ps -AlFH` threads  

 `/proc` is a virtual file system  
  Files:  
  `cmdline` – command line of the command.  
  `environ` – environment variables.  
  `fd` – Contains the file descriptors which is linked to the appropriate files.  
  `limits` – Contains the information about the specific limits to the process.  
  `mounts` – mount related information  
  Links:  
  `cwd` – Link to current working directory of the process.  
  `exe` – Link to executable of the process.  
  `root` – Link to the root directory of the process.  
