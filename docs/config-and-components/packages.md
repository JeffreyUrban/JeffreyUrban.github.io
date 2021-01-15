---
title: Packages
parent: Config & Components
---

RPM-managed:  
  General:  
   Prefer `yum` over `rpm` to resolve dependencies, etc.  
  Verify package database:  
   `/usr/lib/rpm/rpmdb_verify /var/lib/rpm/Packages`  
  List installed packages:  
   `yum list installed`  
  Update package list:  
   `yum check-update`  
  Rebuild package list cache:  
   `yum makecache`  
  Info about package:  
   `yum info`   
  Search for package:  
   `yum search`   
   Search including disabled repos:  
    `yum --enablerepo= search`   
  Check for excluded packages \(will not be available for search or install\):  
   `/etc/yum.conf`  
  Install package:  
   `yum install -y`   
   `rpm -Uvh`   
   Lock in version:  
    Install `versionlock`:  
     `yum install -y yum-plugin-versionlock`  
    Lock version:  
     `yum versionlock add`   
    Check locked versions:  
     `yum versionlock status`  
  Package that is source of file:  
   `rpm -qf /etc/`  
   `yum provides`  
  All files sourced from package:  
   `rpm -ql`   
  Source package for command \(need not yet be installed\):  
   `yum whatprovides`
   `apt search`   
  List all files that are or will be installed by a package:  
   `repoquery -l`   
  List systemd services installed by a package:  
   `repoquery -l  | grep systemd`
  Check dependencies:  
   `yum deplist`   
  Downgrade:  
   `yum downgrade`   
  Verify package:
   Install verify:  
    `yum install -y yum-plugin-verify`  
   Verify package:  
    `yum verify`   
   `rpm -V`  \# Lists changed files of package  
  Fix package:  
   Set permissions, IDs:  
    `rpm --setperms`   
    `rpm --setugids`   
   Reinstall:  
    `yum reinstall`   
 APT-managed:  
  Search for package:  
   `apt-cache search pidstat`  

 List intentionally installed packages  
  Reference: [https://askubuntu.com/questions/17823/how-to-list-all-installed-packages](https://askubuntu.com/questions/17823/how-to-list-all-installed-packages)  
  Listed as:  
   Commandline:
```
    apt-get install \   
    (zcat $(ls -tr /var/log/apt/history.log.gz); cat /var/log/apt/history.log) 2>/dev/null |  
    egrep '^(Start-Date:|Commandline:)' |  
    grep -v aptdaemon |  
    egrep '^Commandline:'  
```
TODO: Check against original notes.

   Start-Date:   
   Commandline:
```
    apt-get install   
    (zcat $(ls -tr /var/log/apt/history.log\*.gz); cat /var/log/apt/history.log) 2>/dev/null |  
    egrep '^(Start-Date:|Commandline:)' |  
    grep -v aptdaemon |  
    egrep -B1 '^Commandline:'  
```
TODO: Check against original notes.

 Use fastest mirror:  
  yum  
   Use fastest mirror dynamically on-demand:  
    `fastestmirror` \# [https://wiki.centos.org/PackageManagement/Yum/FastestMirror](https://wiki.centos.org/PackageManagement/Yum/FastestMirror)  
  apt  
   Find fastest mirrors to use in `/etc/apt/sources.list`  
    `netselect-apt` \# [https://www.unixmen.com/find-fastest-mirror-debian-derivatives/](https://www.unixmen.com/find-fastest-mirror-debian-derivatives/)  
   Find fastest mirror and update `/etc/apt/sources.list`  
    `apt-spy` \# [https://benohead.com/debian-using-apt-spy-to-find-the-fastest-archive-mirror/](https://benohead.com/debian-using-apt-spy-to-find-the-fastest-archive-mirror/)  

 apt  
  Use `apt`, not `apt-get` for basics. See [https://itsfoss.com/apt-vs-apt-get-difference/](https://itsfoss.com/apt-vs-apt-get-difference/)  

Search apt for executable:
  apt-file search --regexp 'bin/<name>$'

Clean apt cache
  sudo apt autoclean

apt-mirror sync
	`rsync apt-mirror`
		Check for permission error files
			-> just `apt-mirror/.gnupg/` ignoring for now.
	Set up on server
		uncomment the line in `</etc/cron.d/apt-mirror>` to enable daily mirror updates
			No. Make systemd timer instead.
				`/usr/bin/apt-mirror > /home/jurban/data/apt-mirror/var/systemd.log`
				Update `/etc/cron.d/apt-mirror` to point to systemd service and timer
		Add (for RasPi):
			`http://mirrors.ocf.berkeley.edu/raspbian/raspbian buster/main armhf`
		Add mirrors for regular ubuntu, NVIDIA stuff
			`http://ppa.launchpad.net/graphics-drivers/ppa/ubuntu bionic/main amd64`
			`http://apt.pop-os.org/proprietary bionic/main all`
	Relevant files:
		`/usr/bin/apt-mirror`
		`/etc/apt/mirror.list`
	Run manually as:
		`sudo su - apt-mirror -c apt-mirror`
	Tutorial:
		https://www.howtoforge.com/local_debian_ubuntu_mirror
	Tool to try for mirror speed comparison:
		https://github.com/jblakeman/apt-select

Ubuntu Automatic updates
	https://libre-software.net/ubuntu-automatic-updates/

