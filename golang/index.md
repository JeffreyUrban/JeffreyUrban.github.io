---
title: Golang
---

# Install

As of 2021-01-16 on amd64, snap install is latest (1.15.6), whereas apt package is almost a year old (1.13.8).

`sudo snap install go --classic`

# Other 

Strings are defined with double-quotes "" only, not single quotes ''.

Use `defer` to avoid duplicating code for each return in case of multiple returns.

Parameters are pass-by-value. 

Pointer syntax is similar to C.

Strings can change length, without changing the pointed string variable address. 
