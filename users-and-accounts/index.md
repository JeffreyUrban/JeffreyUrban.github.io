---
title: Users & Accounts
---

Operate as other user:  
  General  
   Prefer `sudo` \(more limited\) over `su`  
  `sudo`  
   Authorized user list:  
    `/etc/sudoers`  
    `visudo`  
   Avoid needing passwords for `sudo`  
    `sudo visudo`  
     Remove line: `<username> ALL=(ALL) ALL`  
     Add line at end: `<username> ALL=(ALL) NOPASSWD: ALL`  
  `su`  
   General  
    Best to use full path to `su`, to avoid sending password through fake `su` in search path.  
    `su` limited to `wheel` group members  
   Non-login mode \(uses `~/.bashrc` only\):  
    `su`   
   Login mode \(uses `~/.bash\profile` which calls `~/.bashrc`, better for diagnosing user problems\):  
    `su -`   
 Lock an account \(prevent any password from hashing\):  
  `passwd -l` \# prepends password hash with `!`  

 Logged in users:  
  `who`  
  `w`

## New user:

`useradd -m <username> -c "<GECOS field>"`   
_\# -m: Create home directory if doesn't exist._  
`passwd <username>`  
`adduser <username> sudo`

## To Organize

`psacct` or `acct` tools are very useful for monitoring each users activity  

 `id`: Check user ID info  

 Become root with logon shell:  
  `sudo su -`  



Make home directory for existing user: `mkhomedir_helper <username>`

Add user to group:
	`sudo usermod -a -G <groupname> <username>`
	(log out and back in)

Linux run user and group(s) can differ from full set for a user:
	https://unix.stackexchange.com/questions/206289/how-do-linux-permissions-work-when-a-process-is-running-as-a-specific-group

Create / recreate home folder:
	https://askubuntu.com/questions/335961/create-default-home-directory-for-existing-user-in-terminal
