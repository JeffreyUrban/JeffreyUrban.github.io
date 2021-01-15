---
title: Text Streams
parent: Shell
---

Streams  
  `grep`  
   `-v`: invert  
   `-e`: multiple select  
   `-r`: recursive \(directory\)  
  Combine `stdout` and `stderr`: `2>&1`  
  `head`  
  Align columns:  
    `| sed 's/l/ /g' | column -t`  

 Unique word count in file(s):  
  `cat  | sed 's/\n/\n/g' | tr -c [:alnum:]- ' ' | tr ' ' '\n' | sort | uniq -c | sort -nr`  
 `cut`  
  Cut on space and output 9th field:  
   `cut -d ' ' -f9`  
 `sed`  
  Combine commands  
   `sed ';'`  
  Remove prefix that may include timestamp, etc:  
   `sed 's/. //g'`  
  Remove lines with string:
   `sed '//d'`  
  Split into lines upon delimiter:
   `sed 's//\n/g'`
  Reverse order around delimiter:
   `sed 's//\n/g' | tac | sed ':a;$!{N;ba};s/\n//g'`  
  Modify file in place (`-i`), deleting line (`/d`):  
   `sed -i '//d'`   

 Unique word count:
 `cat  | sed 's/\n/\n/g' | tr -c [:alnum:]- ' ' | tr ' ' '\n' | sort | uniq -c | sort -nr`  

 Start with basic word count, relative word count
  Example syslog unique word count:
   `cat syslog | sed 's/\n/\n/g' | tr -c [:alnum:]- ' ' | tr ' ' '\n' | sort | uniq -c | sort -nr`  
   Start building a parser. Start by removing boilerplate and looking for consistency in line pattern.  
    `cat syslog | sed 's/\n/\n/g'`  
   Combine syslogs for analysis
    `cat syslog`  
   Filter prefix of each original line
    `sed 's/.\*  //g'`  

 Sed  
  Remove last character in each line:  
   `sed 's/.$//'`
  Reverse order around delimiter string  
 \(useful to put timestamp and data last, in order to avoid buffering: process them only if an entry has changed\).  
 ---  
   `sed 's//\n/g' | tac | sed ':a;$!{N;ba};s/\n//g'`  
  Split lines on delimiters:  
   `sed 's//\n/g;s//\n/g'`  

 Align columns  
  pipe through: `sed 's/l/ /g' | column -t`  

Filter out full-line \#-delineated comments: `grep "^"`  
Filter out comments and blank lines: `grep -v '^$\|^\s*\#'`  

Multi-line pattern match:
	`awk '{if ($0 ~ /Start pattern/) {triggered=1;}if (triggered) {print; if ($0 ~ /End pattern/) { exit;}}}' filename`
