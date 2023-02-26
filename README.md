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

`du` is used to find information on disk usage. If you want to find disk usage information for a particular folder you can use `du {folder}`.

Some of the most used flags are:

`du -h`: Gives output in human readable format.
`du -h -m`: Gives output in MB in a human readable format. 

`df` is used to find information on free disk space. df gives you an output for all mounted disk on the system. 

Some of the most used flags are:

`df -h`: Gives output in human readable format. 
`df -h --total`: You can use this option when all mounted filesystem are on the same system.

### `rsync`

This command is used to transfer a file/directories to a remote location over a remote shell. It is fast and provides incremental transfer by only transferring the difference between source and destination. 

This is pre-installed tool depending on your Linux distro, but if not it can be easily installed using your distribution package manager `sudo apt install rsync` or `sudo yum install rsync`

The basic syntax of rsync command is `rsync options source destination`

Some of the commonly used flags in rsysnc are: 

-v: verbose
-r: copies file recursivelt
-a: archive mode
-z: compress file data
-h: human readable format
--max-size: Set the max size for file transfer
--include: you could use it for file extenstion '*.txt'
--exlude: can be used to exclude file
--remove-source-files: remove source file after rsync is complete
--dry-run

In the following example, we are copying file from existing directory into a new directory

`rsync -zvh file1 fold1/`
If the destination does not exists, rysync will create that destination folder as well. 

To copy a file on a new machine, you can use the following command: 
`rsync -avzh /fold1 root@192.168.0.1:/root/`
This will copy the content of the folder in the home directory of root user. 

To copy a file from a remote server using sshm you can use the following command: 
`rsync -avzhe ssh root@192.168.0.1:/root/file1 /tmp`

It's highly recommended to use dry run before you rsync, the output will tell you what will be synced across:
`rsync --dry-run -zvh source destination`
### `top`

This command will show you the list of Linux processes. This is supposed to be a summary page and as soon as you type `top`, it will show you a dashboard of running processes in the Linux Kernel. You can type q to quit from the summary page. 

The following columns are shown in the top dashboard: 

-PID: Task unique process ID
-PR: Process priority, the lower the number the higher is the priority
-VIRT: Total virtual memory used by the task
-USER: Owner of the task
-%CPU: CPU usage
-TIME: CPU time
-SHR: Shared memory in KB used by a task
-NI: Nice value of a task, a negative NIC implies higher priority and positive NI represents lower priority. 
-%MEM: Memory usage of a task
-RES: How much physical RAM is the process using
-COMMAND: The name of the command that stated the process. 

This [link](https://www.redhat.com/sysadmin/interpret-top-output) has all the detailed informaton on what the first 4 lines of the summary page. 

Some of the most used commands are listed below

`top -u suhail`
This command will list all the process for the user Suhail

`top -s`
Runs in secure mode

### `ps`

This command is used to display or view information related to processes running in a Linux system. The output of PS will have the following output

-PID: Unique process ID
-TTY: The type of terminal that the user is logged into
-Time: Time for which the process has been running for
-CMD: The command that launches the process. 

Some of the commonly used commands are listed below:

`ps ax` This will display all current running processes
`ps aux` This will display the processes in BSD format
`ps -ef` This will display the processes in full format list
`ps -u suhail` This will diplay processes for user suhail
`ps -fG group_name`: This will display processe for a group

### `lsof`

### `uptime`

This is simple command which tells you the system uptime. 

Some of the commonly used uptime commands are:

`uptime -p`: Pretty flag
`uptime -s`: Uptime since
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


