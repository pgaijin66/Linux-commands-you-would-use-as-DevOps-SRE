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

This command displays the amount of free and used memory of a system. In other words, it gives you a summary of phyiscal and swap memory, as well as free and used memory. Swap is a space on the disk which is used when the amount of physical RAM is full. By default swap partition is not present and only has swap files. 

These are the fields that shows up by default: 

* total: Total memory which can be used by the application
* used: Total memory which has been used `total - free - buffers - cache`
* free: Free memory
* shared: NA
* buff/cache: `-w` flag can dissect buff/cache into buffer and cache separately. More about buffer and cache below.
* available: An estimate of total memory which be used for new application. 

Cache is used to store frequent data whereas buffer is used only once to improve the efficiency of the process such as data transfer. 

There are multiple flgs you can use with `free` without any flags it will give the output in kilobytes. 

Some of the frequently used flags could be: 

`free -m`: Gives you the output in MB
`free -h`: Gives the output in human readable format

### `du / df`

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


