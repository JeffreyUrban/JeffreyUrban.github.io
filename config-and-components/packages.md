---
title: Packages
parent: Config & Components
---

# RPM-managed:  

## Package manager:  
Prefer `yum` over `rpm` to resolve dependencies, etc.  

## Verify package database:  
`/usr/lib/rpm/rpmdb_verify /var/lib/rpm/Packages`  

## List installed packages:  
`yum list installed`  

## Update package list:  
`yum check-update`  

## Rebuild package list cache:  
`yum makecache`  

## Info about package:  
`yum info`   

## Search for package:  
`yum search`

### Search including disabled repos:  
`yum --enablerepo= search`   

## Check for excluded packages \(will not be available for search or install\):  
`/etc/yum.conf`  

## Install package:  
`yum install -y`   
`rpm -Uvh`   

### Lock in version:  
#### Install `versionlock`:  
`yum install -y yum-plugin-versionlock`  
#### Lock version:  
`yum versionlock add`   
#### Check locked versions:  
`yum versionlock status`  

## Identify package that is source of file:  
`rpm -qf /etc/`  
`yum provides`  

## List all files sourced from package:  
`rpm -ql`   

## Identify source package for a command (need not yet be installed):  
`yum whatprovides`

## List all files that are or will be installed by a package:  
`repoquery -l`   

## List systemd services installed by a package:  
`repoquery -l  | grep systemd`

## Check dependencies:  
`yum deplist`   

## Downgrade:  
`yum downgrade`   

## Verify package:
### Install verify:  
`yum install -y yum-plugin-verify`  
### Verify package:  
`yum verify`   
`rpm -V`  _(Lists changed files of package)_

## Fix package:  
### Set permissions, IDs:  
`rpm --setperms`   
`rpm --setugids`   
### Reinstall:  
`yum reinstall`   

## Use yum fastest mirror dynamically on-demand:  
`fastestmirror` 

[Reference](https://wiki.centos.org/PackageManagement/Yum/FastestMirror)

# APT-managed:  

Best to use `apt`, not `apt-get` for basics. [Reference](https://itsfoss.com/apt-vs-apt-get-difference/)

## Search for package:  
`apt-cache search pidstat`  

## List intentionally installed packages  
[Reference](https://askubuntu.com/questions/17823/how-to-list-all-installed-packages)  

```
apt-get install \   
	(zcat $(ls -tr /var/log/apt/history.log.gz); cat /var/log/apt/history.log) 2>/dev/null |  
	egrep '^(Start-Date:|Commandline:)' |  
	grep -v aptdaemon |  
	egrep '^Commandline:'  
```

## Identify source package for a command (need not yet be installed):
`apt search`

## Use fastest mirror:  

### Find fastest mirrors to use in `/etc/apt/sources.list`  

`netselect-apt` 
[Reference](https://www.unixmen.com/find-fastest-mirror-debian-derivatives/)  

### Find fastest mirror and update `/etc/apt/sources.list`  

`apt-spy`

[Reference](https://benohead.com/debian-using-apt-spy-to-find-the-fastest-archive-mirror/)  

## Search apt for executable:

`apt-file search --regexp 'bin/<name>$'`

## Clean apt cache

`sudo apt autoclean`

## APT Mirror

[Tutorial](https://www.howtoforge.com/local_debian_ubuntu_mirror)

Sync with mirror: `rsync apt-mirror`

### Set up on server

#### Enable daily updates

Don't: uncomment the line in `</etc/cron.d/apt-mirror>`

Do: Make systemd timer.

`/usr/bin/apt-mirror > /home/jurban/data/apt-mirror/var/systemd.log`

Update `/etc/cron.d/apt-mirror` to point to systemd service and timer

#### Repos to mirror

(for RasPi): `http://mirrors.ocf.berkeley.edu/raspbian/raspbian buster/main armhf`

For regular ubuntu, NVIDIA stuff
`http://ppa.launchpad.net/graphics-drivers/ppa/ubuntu bionic/main amd64`
`http://apt.pop-os.org/proprietary bionic/main all`

### Relevant files:

`/usr/bin/apt-mirror`
`/etc/apt/mirror.list`

### Run manually as:

`sudo su - apt-mirror -c apt-mirror`

## Other APT

[Tool to try for mirror speed comparison](https://github.com/jblakeman/apt-select)

[Ubuntu Automatic updates](https://libre-software.net/ubuntu-automatic-updates/)
