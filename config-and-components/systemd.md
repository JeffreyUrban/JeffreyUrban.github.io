---
title: systemd
parent: Config & Components
---

List all loaded and active services, sockets, targets, mounts, and devices, with status:  
  `systemctl`  
 Configuration:  
  `/etc/systemd/system/`  
 Standard targets:  
```
  poweroff.target  
  emergency.target  
  rescue.target  
  multi-user.target  
  graphical.target  
  reboot.target  
```
 Available targets:  
  `systemctl list-units --type=target`  
 Activate target \(a unit and its dependencies alone\):  
  `systemctl isolate`   
 Default target \(for boot\):  
  Check:  
   `systemctl get-default`  
  Set:  
   `sudo systemctl set-default`   

 `systemd`  
  Unit naming convention  
   .  
  ---  
  Show tree of services registered with systemd, by control group  
   `systemd-cgls`  
  Show cgroup and service resource usage  
   `systemd-cgtop`  
  More info on systemd resource management  
   `man systemd.resource-control`  
  List active units  
   `systemctl list-units`  
   ---  
   Flags:  
    `-t` : filter by type  
  List unit files  
   `systemctl list-unit-files`  
  View unit file location and content  
   `systemctl cat`   
  Customize unit files  
   Must change only `/etc/systemd/system` directory  
    Overrides corresponding default unit file  
   Modify  
    `systemctl edit`  \# Safer than performing these steps manually:  
     Adds `/etc/systemd/system/.d/` directory  
     Includes only changed lines in `/etc/systemd/system/.d/.conf`  
    ---  
    Configuration for a process that always comes back to life:  
 ```
     [Unit]  
     Description=  

     [Service]  
     Type=simple  
     User=  
     ExecStart=  
     WorkingDirectory=  
     Restart=always  

     [Install]  
     WantedBy=multi-user.target  
```
   Replace  
    `systemctl edit --full`   
   Reload \(activates modification or replacement without needing a reboot\)  
    `systemctl daemon-reload`  
  View unit file changes  
   `systemd-delta`  
  Help on unit  
   `systemctl help`  \# q cycles to next help page \(if multiple sources\)  
   ---  
   Flags  
    `-H` : Manage a remote system  
  Target  
   Change active target  
    `systemctl isolate`   
   Check default  
    `systemctl get-default`  
   Change default  
    `systemctl set-default`   
   Documentation  
    `systemd.target, systemd.special`  
  Service  
   Reload configuration file \(to apply changes\)  
    `systemctl reload`   
   Check if active \(useful for script\)  
    `systemctl is-active`   
   Prevent from starting  
    `systemctl mask`  \# links service unit file to `/dev/null`  
    Unmask:  
    `systemctl unmask`   
  Check boot time \(for kernel and userspace\)  
   `systemd-analyze`  
   Running units by time  
    `systemd-analyze blame`  
   Longest chain or chain for specific units  
    `systemd-analyze critical-chain`   
    As a boot plot  
     `systemd-analyze plot > .svg`
     ---  
     Flags  
      `-H username@host`: on remote host  
  `journalctl`  
   Logs stored in: `/run/log/journal/`  
   Make log files persistent \(by default are flushed on reboot, since in /run\)  
    `mkdir -p /var/log/journal`  
    `systemd-tmpfiles --create --prefix /var/log/journal`  
    ---  
    Caution: generates lots of data  
   Configuration: `/etc/systemd/journald.conf`  
    \(storage locations, compression, max size, max file size, retention time\)  
   View logs:  
    `journalctl \(command\)`  
    ---  
    Flags:  
     `-r`: sort newest entries first  
     `-e`: jump to end  
     `-n` : most recent n entries  
     `-f`: follow new entries  
     `-u` : limit entries to one unit  
     `-o` : format output  
      `verbose`: Full database dump of entries  
      `json-pretty`: JSON structure for parsing  
     `-x`: show explanations with links to documentation  
     `-k`: limit to kernel and to current boot session \(similar to dmesg\)  
     `-b`: limit to current boot session  
     `--list-boots`: list boot sessions \(if log files are persistent\)  
     `-b` : limit to specified boot session  
      Present boot is 0, previous boot is -1, ...  
     `--since`   
     `--until` :  
      `timestamp: YYYY-MM-DD HH:MM:SS`  
      `descriptor`: `yesterday` / `today` / `now` ...  
     `--disk-usage`: show storage used \(if log files are persistent\)  
     `--rotate`: force log rotation \(returns only when rotation is complete\)  
    Field meanings:  
     `man 7 systemd.journal-fields`  
   Write to journal  
    `echo "My journal entry" | systemd-cat` # recorded as process 'cat'  
  Timers  
   List timers  
    `systemctl list-timers --all`  
   Each .timer unit file must have a matching `.service` unit file  
   Transient timer  
    `systemd-run --on-active=`   
     \# Does not require service file  
   Non-transient timer  
    Monotonic timer  
```
     .timer:  # (runs .service)  
      [Unit]  
      Description=  
      Documentation=()>  

      [Timer]  
      OnBootSec=  
      OnUnitActiveSec=  
```
TODO: Check against original notes

    Realtime timer  
```
     .timer  # (runs .service)  
      [Unit]  
      Description=  
      Documentation=()>  
       # Use  _for time wildcard  
      [Timer]  
      OnCalendar=-- ::  
      Persistent=true  # Run immediately if missed (such as system was off)  
      Unit=.service  

      [Install]  
      WantedBy=  
```
TODO: Check against original notes

    Enable  
     `systemctl enable`   
    Start  
     `systemctl start`   

  `systemd` containers: `systemd-nspawn` \(great for sandbox environments\)_  
   Includes the systemd init system within each container.  
    Uses system resources.
    Does not require it's own file system, BIOS, device drivers, etc.
    Container itself is manageable as a service.
    ---  
    Create a container:
     Place bootable OS tree or image in /var/lib/machines/
     Pull image from online repo:
      `machinectl pull-raw --verify=checksum`  # for raw disk image
       # Similar for other formats
      Linux distro-specific tools allow pulling specific releases by number
       to install CentOS image:
       to install Debian image:
        (install package: `debootstrap`)
        `debootstrap --arch=  /var/lib/machines/`
    Spawn command or OS in new container:
     Prerequisites:
      RHEL-based host: Must set SELinux permissive mode via `setenforce 0`
     `systemd-nspawn`
     ---  
     [https://www.freedesktop.org/software/systemd/man/systemd-nspawn.html](https://www.freedesktop.org/software/systemd/man/systemd-nspawn.html)  
     Flags:
      `-D` : specify directory
      `-M` : Specify name for use with machinectl and hostname \(can be overridden\)
      Networking options:
       \(no flag\): Shared virtual interface b/w container and host
       `-b`: No private networking
       `--private-network`: No network connection to or through host \(good for SW testing\)
       `--network-veth`: Shared virtual interface b/w container and host, per configuration
        # Container services and applications can bind to any port that the host hasn't already.
        # Requires `systemd-networkd.service` within container \(pre-installed and enabled on Debian-based systems\).
        # Requires connections to be configured in `/etc/systemd/network/.network`. Network devices configured in `/etc/systemd/network/.netdev`. Documentation in: `systemd.link`, `systemd.netdev`, `systemd.network`.
       `--network-bridge=`: Attach to an existing network bridge on the host
       `--network-interface=`: Designate a host network interface for container's exclusive use
        # Interface will be unavailable to host while container is powered on
      Network configuration \(`.network`\) file:  
```
       [Match]  
       Name=ve-  # Name format for interface  
       [Network]  
       Address=0.0.0.0/28  # 0s are OK, since Systemd will assign an available network range  
       DHCPServer=yes  # Host provides DHCP for container to select IP  
```
     Upon starting container:  
      _Caution_: If Debian container, before exiting, install dbus:  
       `apt install dbus`  
      Set root password:  
       `passwd`  
      If `pam\securetty` installed, it must be removed or renamed in the container  
       `mv /etc/securetty /etc/securetty.disable`  
      Exit and kill container:  
       `control-]` three times  
     ---  
    Start existing container \(in background\):  
     `machinectl start`   
    Enable container:  
     `machinectl enable`   
      \# Same as: `systemctl enable systemd-nspawn@.service`  
     ^^^ what is difference between these methods?  
    Manage container:  
     `machinectl`    
      Commands: `list`, `list-images`, `login`, `status`, `reboot`, `poweroff`, `start`, `enable`, `remove`  

 Locale and keyboard mapping \(systemd\): view, update  
  `localectl`  
 System time \(systemd\) \(including local, UTC, RTC, time zone, NTP status\)  
  `timedatectl`  

 Check all running systemd services with `systemctl`  

 Services listed in: `/etc/systemd/system/multi-user.target.wants`

## Create task that runs on startup and automatically restarts

[Reference](https://medium.com/@benmorel/creating-a-linux-service-with-systemd-611b5c8b91d6)

`/lib/systemd/system/<name>.service`
```
[Unit]  
Description=<description>  

[Service]  
Type=simple   
User=<user>   
ExecStart=<command-line w/full path>   
WorkingDirectory=<path>   
Restart=always  
RestartSec=<seconds to wait before restart attempts>  
StartLimitIntervalBurst=<number of restart attempts>  
StartLimitInterval=0  

[Install]   
WantedBy=multi-user.target
```

Note: systemd will disable a service if it fails or restarts more than 5 times within 10 seconds.  
Setting `StartLimitInterval=0` resets this count, preventing the service being disabled.

`sudo systemctl enable ssh-tunnel.service`  
`sudo systemctl start ssh-tunnel.service`
