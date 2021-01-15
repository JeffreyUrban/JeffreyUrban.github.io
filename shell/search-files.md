---
title: Search Files
parent: Shell
---

Find command:  
  Path to executable command \(within search path\):  
   `which`  
  Binary, source, and manual page files for a command \(beyond search path\):  
   `whereis`  

 Find files matching pattern:  
  `locate`  
   Update file database:  
    `updatedb`  
 Apply command to files matching pattern:  
  `find  -iname  | while IFS= read -r line; do  "$line"; done`  
  E.g. Remove files starting with `.`:  
   `find . -iname . | while IFS= read -r line; do rm "$line"; done`  

 Search directory contents for string \(report files\):_  
  `grep -iRl ""`   

 Searching for commands in scripts_  
  `grep ro <script>|grep <command>`  
   `ro` is for read-only filesystem?  

 `ag`: Silver search  
