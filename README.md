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

This command will list all open files (as per man)

Some of the most used commands are below:

`lsof -u suhail`: Displays open file for user suhail
`lsof -i TCP:22`: Displays process running on specific port 22
`lsof -i 4`: Shows IPv4 network files opened, 6 can be used for IPv6
`lsof -i TCP:1-1024`: Open files of TCP Port range from 1-1024
`lsof -i -u^root`: Exclude a particular user root
`lsof -i`: Shows the list of all network connections `Listening and Established`
### `uptime`

This is simple command which tells you the system uptime. 

Some of the commonly used uptime commands are:

`uptime -p`: Pretty flag
`uptime -s`: Uptime since
### `dmesg`

This will display kernel-related messages used to control Kernel ring buffer. The output contains messages produced by the device drivers. 

This [link](https://www.howtogeek.com/449335/how-to-use-the-dmesg-command-on-linux/) has detailed explanation on how Linux's Ring Buffer works. 

dmesg has to be used with root privleges

Some of the frequently used commands are: 

`sudo dmesg -l info` Extracting messages using -l level to list all informational messages
`sudo dmesg -l debug,notice` Extracting messages (combining debug and notice) to extract debug and notice 
`sudo dmesg --level=err,warn` Extracting messages with error logs and warning messages
`sudo dmesg | grep -i eth0` Extracting message for eth0 user interface

### `netstat`

This command gives you information about network connections, the ports that are in use, and the processes which are using them. 

If this tool is not installed, you can install it by using the command

`sudo apt install net-tools` (Debian)

Some of the commonly used netstat commands are listed below:

`netstat -a` Output all connected and waiting sockets
`netstat -at` All TCP connection
`netstat -au` All UDP connection
`netstat -l` Sockets that are in listening state
`netstat -st` Statistics options with TCP
`netstat -p -at` Shows process names and PID
`netstat -r` This shows the routing table
`netstat -i` Shows all network interfaces

### `ss`

As per man, this is another tool to investiage sockets on a Linux machine. This is used for gathering network information and troubleshooting network issues. 

The output of `ss` will list down all the open sockets (non listening) with established connections. 

The output column shows the following:

* Netid: Type of socket, TCP, UDP, u_str (Unix stream),  u_seq (Unix sequence)
* State: Listening, Established
* Recv-Q: Packets Received
* Send-Q: Packets sent
* Local address port: Address of local machine and port
* Peer address port: Remote machine and port

Some of the commonly used `ss` commands is listed below: 

`ss -a` : Shows all listening and non-listening connections
`ss- l`: Shows listening sockets
`ss -t`: Shows TCP connections
`ss -u`: Shows UDP connections
`ss dst 1.1.1.1`: Filters by destination IP
`ss src 1.1.1.1`: Filters by source IP
`ss -p`: Shows process ID use

SS Vs netstat: SS seems to be a popular tool for networking stats and can also be seen as an alternative to netstat, it is lightweight, faster and has better filtering options. 

### `strace`

This command will trace for system calls and signals (as per man). This command is useeful when the source code is not readily available and can be used to intercept and records any syscall made by a command. 

For example if you type `strace ls`, it will intercept and records all syscalls made by this command. 

Some of the widely commands are listed below: 

`strace -t whoami`: Records timing and duration information
`strace -c whoami`: Gives statistics and reports it

You can also format the output and use regex expressions with strace

`strace -e trace=fstat whoami`: This filters to output only fstat syscalls. 
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


