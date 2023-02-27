# Linux commands that you should know as a DevOps / SRE

As a DevOps / SRE, having a strong understanding of Linux commands is essential to the job. Common Linux commands like ls, cd, rm, mkdir, and sudo can be used in various scripts to make changes and manage systems. Additionally, having a good grasp of grep, find, xargs, and sed can help to search for, extract, and manipulate various types of data. Learning how to use the apt-get and yum package managers can also be beneficial for managing installed applications, as well as more advanced commands such as iptables, systemctl, and firewalld to control security and manage services. Lastly, having knowledge of SSH and SCP can help to securely access remote systems and transfer files.

The following are the commands that you would beed to be aware and have a good handle.

# Table of contents

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
- [Contributing](#contributing)
- [Our Contributors](#our-contributors)

## Commands

### `free`

#### Description

man page - [free](https://man7.org/linux/man-pages/man1/free.1.html)

Fields in free command:

1. total  - Total installed memory (MemTotal and SwapTotal in /proc/meminfo)

2. used  - Used memory (calculated as total - free - buffers - cache)

3. free   - Unused memory (MemFree and SwapFree in /proc/meminfo)

4. shared - Memory used (mostly) by tmpfs (Shmem in /proc/meminfo, available on kernels 2.6.32, displayed as zero if not available)

5. buffers - Memory used by kernel buffers (Buffers in /proc/meminfo)

6. cache  - Memory used by the page cache and slabs (Cached and SReclaimable in /proc/meminfo)

7. buff/cache - Sum of buffers and cache

8. available - Estimation  of  how much memory is available for starting new applications, without swapping. Unlike the data provided by the cache or free fields, this field takes into account page cache and also that not all reclaimable memory slabs will be reclaimed due to items being in use (MemAvailable in /proc/meminfo, available on kernels 3.14, emulated on kernels 2.6.27+, otherwise the same as free)

#### Usage

```shell
$ free -mhw

              total        used        free      shared     buffers       cache   available
Mem:          804Mi       133Mi       476Mi       8.0Mi       0.0Ki       194Mi       531Mi
Swap:         2.1Gi        36Mi       2.0Gi
```

#### Things to know about `free`

1. A healthy system will have `free` memory is nearly close to 0

2. It is okay if `used` memory is close to total

3. Do not panic if `available` memory is less. This means, system is using almost every bit of available memory the memory. Generally 15-20% available memory is a good sign. It means server is performing optimally. If, it is more than that at all time, then server might be overprovisioned. If it is less than 5% or close to 0 at all time, then server might be under provisioned. 

4. If `used` field for `swap` is high or changing, then there might be a change server is paging to disk which is not a good sign. Requires futher investigation.

---

### `du / df`

#### Description

`du` 

Summarize disk usage of each FILE, recursively for directories.


`df`

Displays the amount of disk space available on the file system containing each file name argument.  If no file name is given, the space available on all currently mounted file systems is shown.  Disk space is shown in 1K blocks by default, unless the environment variable POSIXLY_CORRECT is set, in which case 512-byte blocks are used.

If an argument is the absolute file name of a disk device node containing a mounted file system, df shows the space available on that file system rather than on the file system containing the device node.  This version  of  df  cannot  show  the  space  available  on unmounted filesystems, because on most kinds of systems doing so requires very nonportable intimate knowledge of file system structures.

#### Usage

##### `du` with max depth of 3 

```shell
$ du -h --max-depth=3
4.0K	./.ssh
4.0K	./project/.vagrant/rgloader
36K	./project/.vagrant/machines
4.0K	./project/.vagrant/bundler
44K	./project/.vagrant
48K	./project
96K	.
```


`df`

##### Show output in human readable form

```shell
$ df -h

Filesystem                  Size  Used Avail Use% Mounted on
devtmpfs                    384M     0  384M   0% /dev
tmpfs                       403M     0  403M   0% /dev/shm
tmpfs                       403M   11M  392M   3% /run
tmpfs                       403M     0  403M   0% /sys/fs/cgroup
/dev/mapper/rl_rocky8-root  125G  2.9G  123G   3% /
/dev/sda1                  1014M  206M  809M  21% /boot
home_vagrant_project        234G  209G   26G  90% /home/vagrant/project
tmpfs                        81M     0   81M   0% /run/user/1000
```

##### Show number of available inodes

```shell
$ df -ih

Filesystem                 Inodes IUsed IFree IUse% Mounted on
devtmpfs                      96K   344   96K    1% /dev
tmpfs                        101K     1  101K    1% /dev/shm
tmpfs                        101K   492  101K    1% /run
tmpfs                        101K    17  101K    1% /sys/fs/cgroup
/dev/mapper/rl_rocky8-root    63M   67K   63M    1% /
/dev/sda1                    512K   310  512K    1% /boot
home_vagrant_project         1000 -976K  977K     - /home/vagrant/project
tmpfs                        101K     5  101K    1% /run/user/1000
```

#### Things to know about `du/df`

1. `df -ih` can be used to check the number of available inodes allocated to each file system.


---

### `rsync`

#### Description

`rsync` a very versatile tool which can be used to copy files and folders from one directory to another within same file system or to remote.

#### Usage

##### Dry run before actually running

```shell
$ rsync --dry-run local_directory dest_directory
```

##### Differential backup

```shell
$ rsync -av local_directory dest_directory
```

Here `-v` signifies to show output in verbose mode and `-a` means archive, which on first run backs up the data you want, then on the next run, it'll do a block checksum of the file and only copy over the parts which have been modified on existing files, copy new files over and remove fiels which are no longer there. 

##### recursively copy, archive mode, show verbose, use compression, preserve partial files, display progress

```shell
$ rsync -ravzP local_directory dest_directory
```


##### `rsync` over `ssh`

```shell
$ rsync -e ssh local_directory username@remote_server:/path/to/backup_directory
```

##### `rsync` over `ssh` adding other ssh optoins

```shell
$ rsync -e "ssh -i PATH_TO_KEY -o ConnectTimeout=12 -o ConnectionAttempts=18" local_directory username@remote_server:/path/to/backup_directory
```

##### Exclude certain files

```shell
$ rsync -avzP src_directory dest_directory --exclude=".cache"
```

#### Things to know about `rsync`

1. `rsync` is a versatile tool but running it without knowing what the options are used for, can cause some destructive output. So, use `--dry-run` before running your command.

2. `rsync` does not recurse into directories by defaylt. You would need to use `-r` option to recurse or `-a` explicitly which is equivalent of `-rlptgoD`. Expained [here](https://explainshell.com/explain?cmd=rsync+-rlptgoD)

---

### `top`


---

### `ps`


---
### `lsof`


---
### `uptime`


---
### `dmesg`

---
### `netstat`


---
### `ss`


---
### `strace`


---
### `tcpdump`


---
### `sar`


---
### `vmstat`


---
### `iostat`


---
### `pidstat`


---
### `mpstat`


---
### `lscpu`


---
### `uname`


---
### `grep`


---
### `find`


---
### `sort`


---
### `head`


---
### `tail`


---
### `basepath`


---
### `realpath`


---
### `tar`


---
### `sed`


---
### `awk`


---
### `cut`


---
### `tr`


---
### `dig`


---
### `nslookup`


---
### `nc`


---
### `traceroute`


---
### `tracepath`


---
### `ethtool`


---
### `iperf`


---
### `dd`


---
### `ping`


---
### `host`


---
### `tracepath`


---
### `ip`


---
### `uniq`


---
### `diff`


---
### `ssh-keygen`


---
### `ln`


---
### `curl`


---
### `wget`


---
### `atop / htop`


---
### `kill`


---
### `fdisk`


---
### `lsblk`


---
### `mkfs`


---
### `mount / umount`


---
## Contributing

If you've ever wanted to contribute to open source, and a great cause, now is your chance!

To maintain a conistency we recommend this creating a new PR, please add followings:

1. `Description` - short easy to remember description with link to man page.

2. `Usage` - listing out real worl usage which are not easy to find.

3. `Things to know` - List out the gotchas and good to know things about that command

## Our Contributors

Thanks go to these wonderful people:

<a href="https://github.com/pgaijin66/Linux-commands-you-would-use-as-DevOps-SRE/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=pgaijin66/Linux-commands-you-would-use-as-DevOps-SRE" />
</a>