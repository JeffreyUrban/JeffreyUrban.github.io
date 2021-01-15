---
title: Compression (Storage & Transfer)
grand_parent: Storage
parent: Files & Filesystems
---

Split and reassemble file \(i.e. to transfer from OSX to Linux via FAT formatted disk\)  
  Split  
   `split -b 4294967295`    
    \# 1 byte less than 4 GB  
  Reassemble  
   `cat ?? >`   

Read compressed zip file:  
  `zcat`  

 Streaming compression in C, using known dictionary. Lightweight, 10:1 compression ratio.  
  [https://facebook.github.io/zstd/\#small-data](https://facebook.github.io/zstd/#small-data)

## `dtrx`

\(Do The Right Extraction\). Works on a wide variety of compressed file formats.

`sudo apt install dtrx`  
`dtrx <archive>`

##  `tar`

Compress Verbose Zip File

```text
tar -czvf <archive name>.tar.gz <path to directory or file>
```

eXpand Verbose Zip File

 `tar xvzf <filename>.tar.gz`   \# e_x_tract _v_erbose _z_ip _f_ile  

`tar.bz2, tbz2: tar `-j``

## 7z \(7zip\)

```bash
# Install
sudo apt install p7zip-full
# Extract
7z e <archive, or first part of split archive>
```
