---
title: Storage
has_children: true
---

Show disk partitions:  
  `lsblk`  
  `fdisk -l`  
  With UUID and type:  
   `sudo blkid` \(must be root\)  
 Filesystem types and capacities:  
  `df -Th`  
  Note: many filesystems allow ~5% over 100% full for processes running as root.  
 inode usage:  
  `df -i /`  
 Check directory size  
  `du -sh /`  
 Note \(`df` vs `du`\):  
  `df` includes unlinked files still accessed by process \(`du` does not include these\)  
 Disk activity  
  `vmstat -d`  
 Open files  
  `lsof`  
   `-p`   
   `-u`   
   `-i` :  
   \(grep for 'bin', 'log', '.so', etc. to find relevant files\)  
 Specific file \(that may be held by a process, after deleted\)  
  `lsof`   
  `fuser`   
 List file inodes:  
  `ls -i`   
 Find file for inode:  
  `find / -inum`   
 Create file:  
  `dd if=/dev/zero of=file.txt count= bs=`  
  `fallocate -l 1G`   
 Filesystems  
  `ext4`, `xfs`, ...  
  Create filesystem:  
   `mkfs.`   
  Mount filesystem:  
   `mount -t`     
  Remount in write mode:  
   `mount -o rw,remount`   
  Mount on boot:  
   `/etc/fstab`  
  Check `ext2`/`3`/`4` filesystem metadata, including superblocks:  
   `dumpe2fs -h`   
   `dumpe2fs`   
  Repair filesystem:  
   `xfs`:  
    `xfs_repair`   
   `ext4`:  
    `e2fsck -p`  \(follow prompts\)_  
    `fsck.ext4 -y`   
  Resize filesystem:  
   `ext2`, `ext3`, `ext4`:  
    `resizef2s`  // Defaults to expand to fill available space_  
 Files of interest  
  `/dev/zero`  
  `/dev/urandom`  
  `/dev/null`  
 iSCSI  
  Service \(at server\): `target`  
   `port 3260/tcp`  
   Configure:  
    `targetcli`  
  Service \(at client\): `iscsiadm`  
   View nodes:  
    `iscsiadm -m node`  
   Delete nodes:  
    `iscsiadm -m node -o delete`  
   Configuration:  
    `/etc/iscsi/initiatorname.iscsi`  
    `/etc/iscsi/iscsid.conf`  
   Discover target iqns:  
    `iscsiadm -m discovery -t sendtargets -p`   
   Log into client:  
    `iscsiadm -m node -T  -l`  
 Disk encryption  
  Encrypted volumes \(available for `/etc/fstab`\) to decrypt at boot:  
   `/etc/crypttab`  
  Manually decrypt:  
   `cryptsetup luksOpen /dev/mapper/  --key-file`   
  View key slots:  
   `cryptsetup luksDump /dev/mapper/`  
  Restore header \(can fix broken key configuration\):  
   `cryptsetup luksHeaderRestore /dev/mapper/ --header-backup-file`  
 Notify on filesystem events:  
  `inotify-tools`  
  [https://github.com/tinkershack/fluffy\#why-fluffy](https://github.com/tinkershack/fluffy#why-fluffy)  
  [https://github.com/emcrisostomo/fswatch](https://github.com/emcrisostomo/fswatch)

`df` to check disk space

## Mount filesystem from disk image

 List filesystems in image: `sudo fdisk -l <image>`  
    Note:  
     Sector size \(bytes\)  
     Filesystem start \(sectors\)  
     Filesystem type \(Linux is ext4\)  
Mount filesystem:

`mkdir -p <mount-point>`  
`sudo mount -v -o offset=$(( <start> * <sector-size> )),sizelimit=$(( <sectors> * <sector-size> )) -t auto <image> <mount-point>`   
 _Note:_ `sizelimit` _is not required for last partition in image._

Disk read/write speed test:
	https://www.shellhacks.com/disk-speed-test-read-write-hdd-ssd-perfomance-linux/

to reload new entries in `/etc/fstab` use the mount command: `mount -a`
