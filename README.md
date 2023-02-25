# Linux commands that you should know as a DevOps / SRE

The following are the commands that you would beed to be aware and have a good handle.

# Table of contents

- [Commands](#commands)
  - [`free`](#free)
  - [`du / df`](#du--df)
  - [`rsync`](#rsync)
  - [`top`](#top)
  - [`ps`](#ps)
  - [`lsof`](#lsof)
  - [`uptime`](#uptime)
  - [`dmesg`](#dmesg)
  - [`netstat`](#netstat)
  - [`ss`](#ss)
  - [`strace`](#strace)
  - [`tcpdump`](#tcpdump)
  - [`sar`](#sar)
  - [`vmstat`](#vmstat)
  - [`iostat`](#iostat)
  - [`pidstat`](#pidstat)
  - [`mpstat`](#mpstat)
  - [`lscpu`](#lscpu)
  - [`uname`](#uname)
  - [`grep`](#grep)
  - [`find`](#find)
  - [`sort`](#sort)
  - [`head`](#head)
  - [`tail`](#tail)
  - [`basepath`](#basepath)
  - [`realpath`](#realpath)
  - [`tar`](#tar)
  - [`sed`](#sed)
  - [`awk`](#awk)
  - [`cut`](#cut)
  - [`tr`](#tr)
  - [`dig`](#dig)
  - [`nslookup`](#nslookup)
  - [`nc`](#nc)
  - [`traceroute`](#traceroute)
  - [`tracepath`](#tracepath)
  - [`ethtool`](#ethtool)
  - [`iperf`](#iperf)
  - [`dd`](#dd)
  - [`ping`](#ping)
  - [`host`](#host)
  - [`tracepath`](#tracepath)
  - [`ip`](#ip)
  - [`uniq`](#uniq)
  - [`diff`](#diff)
  - [`ssh-keygen`](#ssh-keygen)
  - [`ln`](#ln)
  - [`curl`](#curl)
  - [`wget`](#wget)
  - [`atop / htop`](#atop--htop)
  - [`kill`](#kill)
  - [`fdisk`](#fdisk)
  - [`lsblk`](#lsblk)
  - [`mkfs`](#mkfs)
  - [`mount / umount`](#mount--umount)

## Commands

### `free`

* Displays the total amount of free and used physical and swap memory in the system, as well as the buffers and caches used by the kernel. The information is gathered by parsing /proc/meminfo. The displayed columns are:
```
total  - Total installed memory (MemTotal and SwapTotal in /proc/meminfo)

used  - Used memory (calculated as total - free - buffers - cache)

free   - Unused memory (MemFree and SwapFree in /proc/meminfo)

shared - Memory used (mostly) by tmpfs (Shmem in /proc/meminfo, available on kernels 2.6.32, displayed as zero if not available)

buffers - Memory used by kernel buffers (Buffers in /proc/meminfo)

cache  - Memory used by the page cache and slabs (Cached and SReclaimable in /proc/meminfo)

buff/cache - Sum of buffers and cache

available - Estimation  of  how much memory is available for starting new applications, without swapping. Unlike the data provided by the cache or free fields, this field takes into account page cache and also that not all reclaimable memory slabs will be reclaimed due to items being in use (MemAvailable in /proc/meminfo, available on kernels 3.14, emulated on kernels 2.6.27+, otherwise the same as free)
```

### `du / df`
* du - Summarize disk usage of each FILE, recursively for directories.
* df
```
Displays the amount of disk space available on the file system containing each file name argument.  If no file name is given, the space available on all currently mounted file systems is shown.  Disk space is shown in 1K blocks by default, unless the environment variable POSIXLY_CORRECT is set, in which case 512-byte blocks are used.

If an argument is the absolute file name of a disk device node containing a mounted file system, df shows the space available on that file system rather than on the file system containing the device node.  This version  of  df  cannot  show  the  space  available  on unmounted filesystems, because on most kinds of systems doing so requires very nonportable intimate knowledge of file system structures.
```

### `rsync`

### `top`

### `ps`

### `lsof`

### `uptime`

### `dmesg`

### `netstat`

### `ss`

### `strace`

### `tcpdump`

### `sar`

### `vmstat`

### `iostat`

### `pidstat`

### `mpstat`

### `lscpu`

### `uname`

### `grep`

### `find`

### `sort`

### `head`

### `tail`

### `basepath`

### `realpath`

### `tar`

### `sed`

### `awk`

### `cut`

### `tr`

### `dig`

### `nslookup`

### `nc`

### `traceroute`

### `tracepath`

### `ethtool`

### `iperf`

### `dd`

### `ping`

### `host`

### `tracepath`

### `ip`

### `uniq`

### `diff`

### `ssh-keygen`

### `ln`

### `curl`

### `wget`

### `atop / htop`

### `kill`

### `fdisk`

### `lsblk`

### `mkfs`

### `mount / umount`


