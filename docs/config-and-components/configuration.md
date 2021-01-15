---
title: Configuration
parent: Config & Components
---

## etckeeper

### Install

`sudo apt install etckeeper  
/etc/etckeeper/etckeeper.conf`: `PUSH_REMOTE="origin"`

\(create github repo, share SSH keys for root\)

```text
sudo git remote add origin git@github.com:<repo>.git
sudo git push -u origin master
```

### Work with repository

`cd /etc`  
\(git commands, prefaced with `sudo`\)  

Restore earlier commit in etckeeper and move forward from there (should be similar with git)
  Wasn't clear how to do this, but eventually got there. Relevant commands:
```
    sudo etckeeper vcs reset --soft <commit hash>
    sudo etckeeper vcs clean --dry-run
    sudo etckeeper vcs rebase -i
    sudo etckeeper vcs rebase --continue
```
	Right way to get there:
    https://stackoverflow.com/questions/4991594/revert-a-range-of-commits-in-git
		---
    `sudo etckeeper vcs revert <first_bad_commit>^..<last_bad_commit>`
