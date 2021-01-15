---
title: Vim
---

Block insert \(such as to comment lines\)  
 ctrl-v \# Enter visual block mode  
 \(move\) \# To form block  
 shift-i \# Begin insert  
 \(type text\)  
 esc, esc \# Apply to block  
Block remove \(such as to uncomment lines\)  
 ctrl-v \# Enter visual block mode  
 \(move\) \# To form block  
 delete

Save as sudo \(after opening without sudo\): `:w !sudo tee %`

vim
	substitution
		`%s/<find>/<replace>`
