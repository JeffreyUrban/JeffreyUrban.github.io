---
title: Loose Ends
---

Markdown: Add comments:
	Resource:
		https://stackoverflow.com/questions/4823468/comments-in-markdown
	[comment]: <> (This is a comment, it will not be included)

Separate email that is received the same
  Same email with a +N (any int)  before the @ (works on GMail)

Multiple subdomains on nginx
	https://hackprogramming.com/how-to-setup-subdomain-or-host-multiple-domains-using-nginx-in-linux-server/
Grav with the Git-Sync plug-in
	https://learn.getgrav.org/16/webservers-hosting/vps/linode
	https://github.com/hibbitts-design/grav-skeleton-learn2-with-git-sync
	https://learn.getgrav.org/16/webservers-hosting/servers/nginx
	https://getgrav.org/
	https://getgrav.org/blog/git-sync-plugin
	https://learn.getgrav.org/16/cookbook/tutorials/create-a-blog
	---
	Configuration:
		`/etc/nginx/sites-available/grav`
			Configure:
				Root (to match directory location):
					`root /home/grav/www/html/notes.jeffreyurban.com;`
				Webroot subfolder (if using):
```
			    location /<subfolder> {
			        try_files $uri $uri/ /<subfolder>/index.php?$query_string;
			    }
```
				Server Name:
```
					# server_name www.jeffreyurban.com jeffreyurban.com;
					server_name notes.jeffreyurban.com;
```
	`/etc/nginx/nginx.conf`
		`server_tokens off;`  # Hide version from clients
Certbot installation:
	https://certbot.eff.org/lets-encrypt/ubuntubionic-nginx
	---
```
  sudo apt-get update
  sudo apt-get install software-properties-common
  sudo add-apt-repository universe
  sudo add-apt-repository ppa:certbot/certbot
  sudo apt-get update
	sudo apt-get install certbot python-certbot-nginx
	sudo certbot --nginx -d jeffreyurban.com -d www.jeffreyurban.com
	# Answer yes to redirect to https
	# Firewall needs to allow http in order to handle redirect to https
	sudo certbot renew --dry-run

Check if virtualization extensions are enabled
  grep --color -E '(svm|vmx)' /proc/cpuinfo

Lenovo firmware update
  fwupdmgr update

Base 64
  Encode: base64
  Decode: base64 -d

jinja:
	Timestamp:
{% raw %}
		`{% set curtime = None | strftime("%Y.%m.%d.%H.%M.%S") %}`
		{{ curtime }}
{% endraw %}

NFS:
	Unexport a share to <world>:
		exportfs -u *:<path>  # Use '*' where the client IP would be

Jinja filters
	https://docs.saltstack.com/en/latest/topics/jinja/index.html#filters

 Combine all PDFs in a folder \(in listed order\)  
  `pdfunite \*.pdf .pdf`  

minimum \(perfect\) hash \(generate code\):  
  `gperf`  

 Network Time Protocol \(NTP\) client / daemon / server:  
  `chrony`  

 Other tools to consider  
  [http://openxcplatform.com/](http://openxcplatform.com/) Custom applications from vehicle data \(Ford\)  

Also docs.cucumber.io/gherkin  
 Behavioral test language: given X, when Y, then Z  

 Chef may be relevant  
  For configuring test instruments on targets and servers  
  [https://www.chef.sh/about/](https://www.chef.sh/about/)  

  Learn SW tools  
  Jenkins  
  Groovy  
  QTTestLib and GoogleTest  


 Look up Celery tasks in Python  
 Ncolony looks useful for supervising independent test interface processes  
 [http://www.tornadoweb.org/en/stable/](http://www.tornadoweb.org/en/stable/)  
  Networking framework for long lived connections, asynchronous requests  
 Framework on client for REST interface [https://bottlepy.org/docs/dev/](https://bottlepy.org/docs/dev/) [http://flask.pocoo.org/](http://flask.pocoo.org/)  

 Looks interesting / useful?  
  [https://sgframework.readthedocs.io/en/latest/readme.html](https://sgframework.readthedocs.io/en/latest/readme.html)  


 Investigate useful tools for test applications and agents  
  JSON processor: [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/)  
  Event callback library: [https://libevent.org/](https://libevent.org/)  
  Swagger UI: ReST API documentation + GUI interface  


 Other Stack to consider  
  SMACK: Spark, Mesos, Akka, Kafka  
  Storm, Samza, Flink  

Library management:  
  [https://askubuntu.com/questions/40763/symlink-for-dbus-headers](https://askubuntu.com/questions/40763/symlink-for-dbus-headers)  
  [https://ubuntuforums.org/showthread.php?t=388900](https://ubuntuforums.org/showthread.php?t=388900)  
  [http://freesoftwaremagazine.com/articles/brief\_introduction\_to\_gnu\_autotools/](http://freesoftwaremagazine.com/articles/brief_introduction_to_gnu_autotools/)  

 Useful libraries:  
  protobuf, MQTT, JSON, SQLite3, libevent-dev \(event callback\), yaml, uuid-dev, can-utils, mosquitto  

Distributed, fault-tolerant computing abstraction  
  [http://mesos.apache.org/](http://mesos.apache.org/)  
  [http://samza.apache.org/](http://samza.apache.org/)  
  [https://flink.apache.org/](https://flink.apache.org/)  

Android Debug Bridge
    ADB Reference  
     [https://github.com/jackpal/Android-Terminal-Emulator/wiki/Android-Shell-Command-Reference](https://github.com/jackpal/Android-Terminal-Emulator/wiki/Android-Shell-Command-Reference)  
     [https://a3nm.net/blog/android\_cli.html](https://a3nm.net/blog/android_cli.html)  

gpsd
    GNSS instrumentation  
     [http://www.catb.org/gpsd/gpsfake.html](http://www.catb.org/gpsd/gpsfake.html)  
     [http://www.catb.org/gpsd/gpspipe.html](http://www.catb.org/gpsd/gpspipe.html)  
     [http://www.catb.org/gpsd/gpsprof.html](http://www.catb.org/gpsd/gpsprof.html)  
     Docs: [http://www.catb.org/gpsd/](http://www.catb.org/gpsd/)  

Firefox
    ## Disable notifications

    Go to `about:config` in your browser address bar

    `dom.webnotifications.enabled` > `false`

Configuration Management
    Ansible  
     Benefits \(vs Puppet and Chef\):  
      No central server necessary. Can push changes from laptop, etc.  
       Can use server to allow access with permissions  
      Target does not require agent, only ssh and python  

Shared libraries required:  
  `ldd`   
 Update linker cache /etc/ld.so.cache \(after installing or removing shared library\):  
  `ldconfig`  
 Check for memory leak:  
  `valgrind --tool=memcheck --leak-check=full`   
 Trace:  
  System calls:  
   `strace`   
   `strace -p`   
  Shared library function calls:  
   `ltrace`   
   `ltrace -p`   
  File operations only:  
   `strace -e trace=file`  
  Follow forked processes:  
   `strace -f`

## UART Serial Console

### Prerequisite for Ubuntu:

Add user to dialout group due to AppArmor restriction causing permission denied. `sudo usermod --append --groups dialout <username>`

Then log out and back in.

### cu

Connect on serial: `cu -s <baud, e.g. 115200> -l <device, e.g. /dev/ttyUSB0>`

Disconnect \(must be at start of line\): `~.`

# More to organize

sensors
	https://help.ubuntu.com/community/SensorInstallHowto
	---
	Install:
```
		sudo apt install lm-sensors
		sudo sensors-detect
		sudo /etc/init.d/kmod start
```
	Run:
		`sensors`
		---
		See 3 `nouveau-pci-*` entries. Are these the GPUs themselves?
			Temperatures are 28C, 32C, 34C, so perhaps higher ones with less airflow are hotter even when idle.
		---
		Try:
			`psensor`, which includes remote monitoring
			`fancontrol`

Troubleshoot what is changing `/etc/resolv.conf`
	Problem:
		Sites and services (particularly Google) don't work unless I change `/etc/resolv.conf` to nameserver 1.1.1.1
	Insight:
		/etc/resolv.conf as installed was a symlink to /run/systemd/resolve/resolv.conf
		Removing the symlink and adding dns=default to /etc/NetworkManager/NetworkManager.conf results in NetworkManager updating /etc/resolv.conf per the GUI settings.
	How did I leave things (after it seems fixed):
		Followed article:
			https://www.linuxjournal.com/content/have-plan-netplan
			---
			Except case for 'dns' in /etc/NetworkManager/NetworkManager.conf
			Except left systemd-resolved enabled and active
		---
		Left as-is
			`/etc/systemd/resolved.conf`
			`/etc/netplan/`
			`/etc/network/interfaces`
			`/etc/resolvconf/resolv.conf.d/base`
			`/etc/resolvconf/resolv.conf.d/head`
		Settings -> Network -> Wired -> IPv4
			Specified: Manual, fixed IP with self as gateway
		Settings -> Network -> VPN -> IPv4 -> DNS
			Specified: Automatic, DNS 1.1.1.1
		/etc/NetworkManager/NetworkManager.conf
			Added `dns=default` to [main]
			# Article used `DNS=default`. Not sure if case matters.
		`/etc/resolv.conf` is a symlink to `/run/systemd/resolve/resolv.conf`
			Removed symlink, so file is managed by NetworkManager
				NetworkManager is now updating `/etc/resolv.conf` per settings

Ubuntu DNS stuff
	TODO: Distill and document
	---
	Resources to check out:
	->
		`resolvconf`
			`/etc/systemd/resolved.conf`
		`/etc/network/interfaces`
			# `ifupdown` has been replaced by `netplan`(5) on this system.  See
			# `/etc/netplan` for current configuration.
		`/etc/NetworkManager/NetworkManager.conf`
		`dnsmasq`
		`systemd-resolved`
			Provides stub listener on IP address `127.0.0.53`
				-> this is what's broken.
				The DNS servers contacted are determined from:
					1. the global settings in `/etc/systemd/resolved.conf`
					2. the per-link static settings in `/etc/systemd/network/*.network` files
					3. the per-link dynamic settings received over DHCP
					4. any DNS server information made available by other system services.
			Four modes of handling /etc/resolv.conf, selected automatically, depending on if `/etc/resolv.conf` is a symlink to `/run/systemd/resolve/resolv.conf` or lists `127.0.0.53` as DNS server.
		`netplan`
			`/etc/netplan/`
			https://netplan.io/
			https://www.linuxjournal.com/content/have-plan-netplan
				*** Good article ***
				Can configure `netplan` in two ways:
					Use `NetworkManager` (default for desktop Ubuntu):
						interface configuration control is handed off to the GUI interface
					Use `networkd` (default for server Ubuntu):
						`systemd` itself handles the interface configurations
				Author's solution (via `NetworkManager`):
					disable `systemd-resolved`. That has the potential to break DNS lookups in a VPN, but I haven't had an issue with that. With resolved handling DNS information, the `/etc/resolv.conf` file points to `127.0.0.53` as the nameserver. Disabling `systemd-resolved` will stop the automatic creation of the file. Thankfully, `NetworkManager` itself can handle the creation and modification of `/etc/resolv.conf`.
					---
					1. Do `sudo systemctl disable systemd-resolved.service`.
					2. Then `sudo rm /etc/resolv.conf` (get rid of the symlink).
					3. Edit the `/etc/NetworkManager/NetworkManager.conf` file, and in the `[main]` section, add a line that reads `DNS=default`.
					Once those steps are complete, `NetworkManager` itself will create the `/etc/resolv.conf` file, and the DNS server supplied via DHCP or static entry will be used instead of a `127.0.0.53` entry.
				Alternative (`networkd`):
					`/etc/netplan/config.yaml` -> set `renderer` to `networkd` to use the `systemd-networkd` backend.
					E.g.
```
						network:
						  version: 2
						  renderer: networkd
						  ethernets:
						    enp2s0:
						      dhcp4: true
```
Stop `NetworkManager` from managing interface
  `/etc/NetworkManager/NetworkManager.conf`
```
    [keyfile]
    unmanaged-devices=mac:48:2a:e3:58:85:c4
```
List device status
	`nmcli dev status`

Networking resources:
	Reading:
		https://www.serverlab.ca/tutorials/linux/administration-linux/how-to-configure-network-settings-in-ubuntu-18-04-bionic-beaver/
		https://www.linuxjournal.com/content/have-plan-netplan
	Troubleshooting:
		`systemd-resolve --status`

Images
	Command-line tool for image manipulation
		`convert`
Webcam
	command line: http://www.linuxintro.org/wiki/Set_up_a_Webcam_with_Linux
	Applications: `camorama`, `cheese`
Hardware info:
	`sudo apt install hwinfo`
	`hwinfo`
MAC Address:
	Change: `macchanger`
Web hacks:
	https://www.exploit-db.com/
	Google Dorks:
		https://www.exploit-db.com/google-hacking-database
IP location lookup
	`sudo apt install geoip-bin`
	`geoiplookup <ip>`
	Add and update databases in `/usr/share/GeoIP/`
Registration and DNS information
	`whois`
`/etc/apt/sources.list` generator: https://repogen.simplylinux.ch/generate.php

Managing shared libraries:
  https://www.tecmint.com/understanding-shared-libraries-in-linux/
    libraries defined in: `/etc/ld.so.conf`
    When you have just installed new shared libraries or created your own, or created new library directories. You need to run `ldconfig` command to effect the changes.
	Check installed libraries
  	`ldconfig -p`

Set up network time server using `chrony` \(ntp daemon\). Configure `chrony` on clients to access a local time server. Consider forwarding gateway traffic to use the local time server, allowing changing the time on demand. Can set time 0 at beginning of a test suite \(or other level of aggregation\) to more easily compare between runs.  

Reload active user's group assignments without logging out/in
  exec su -l $USER

Reset application paths, such as after moving an application:
  hash -r

Linux:
	Determine which process is listening on a port:
		sudo netstat -tulpn

disk usage, interactive, per-directory
	ncdu

Maximum objects \(open files, processes, signals, queues, etc\)  
 `ulimit -aH`  

## Set hostname

Update in: `/etc/hostname`, `/etc/hosts`  
Reboot system

Embedded Linux Qs to understand system  
  Our system uses  
  What kernel version  
  What distribution?  
  What C library glibc / eglibc / uClibc  
  What debugging, tracing and profiling tools come with \(or are available for\) our toolchain?  
   e.g. Oprofile, memory patrol, linux trace toolkit  
  Includes `gdb` and `gdb-server` \(for target\)? Can we enable these?  
  Do we include another library such as `busybox` or `toybox`? Can / should we for debug?  
  Do we use a commercial BSP \(board support package\), modify one, or did we write our own?  
   Where / how is this patched into kernel?  
  Look for `arch/.config`, `include/linux/autoconf.h`  
  Do we use `udev` \(dynamic device manager\)  
  Are we or can we mount `rootfs` over network?  
   \(for development\) look for `nfsroot`, `root=`  
  What file system do we use?  
   look for `rootfstype`  
  How closely can we mirror the target system on a VM  
   Exclude or simulate hardware that isn't present.  
  Does our target support JTAG or BDM debugging?  
   Are we using it? Should we?  

Load Balancer
    `haproxy`:  
     Vs. NGINX:  
      Is more focused as a load balancer.  
      Comes with monitoring features and hooks for third-party monitoring  
     Supports modes including weighted roundrobin and end-point based selection  

GNU Documentation
  `info`
 For command or conf file:  
  `man`   
 Search all man page names and short descriptions:  
  `man -k "search string"`  
 Package documentation:   
  `/usr/share/doc`  
 Search for `.conf` file documentation  
   `find /usr/share/doc -iname *.conf -type f -print`  
