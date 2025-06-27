# 🐧 Linux Commands Cheat Sheet

## 📁 1. File & Directory Management

| Command | Detailed Description |
|--------|-----------------------|
| `ls` | Lists files and directories in the current working directory. |
| `ls -l` | Lists files with detailed info: permissions, owner, size, modification time. |
| `ls -a` | Includes hidden files (those starting with a dot ., like .bashrc). |
| `cd /path` | Changes current working directory to the specified path. |
| `pwd` | Prints the full path of the current directory (present working directory). |
| `mkdir dirname` | Creates a new directory with the specified name. |
| `rmdir dirname` | Deletes an empty directory; won’t work if directory contains files. |
| `rm file` | Deletes a specified file permanently. |
| `rm -r dirname` | Deletes a directory and its entire contents recursively. |
| `cp src dest` | Copies files or directories from source to destination. |
| `mv src dest` | Moves or renames a file/directory from source to destination. |
| `touch file` | Creates a new empty file or updates timestamp of existing file. |
| `find / -name filename` | Searches entire filesystem for files matching name pattern. |

## 📝 2. File Viewing & Editing

| Command | Detailed Description |
|--------|-----------------------|
| `cat file` | Displays content of a file in terminal (not suitable for large files). |
| `less file` | Opens file in a pager, allows scrolling forward/backward. |
| `more file` | Similar to less, but less flexible (can only scroll forward). |
| `head file` | Shows the first 10 lines of a file (use -n to customize). |
| `tail file` | Shows the last 10 lines of a file (useful for log files). |
| `tail -f file` | Continuously monitors file for changes in real time (e.g., logs). |
| `nano file` | Opens the file in the Nano text editor, beginner-friendly. |
| `vi file` or `vim file` | Opens the file in Vi/Vim editor; powerful and advanced. |

## 🔐 3. File Permissions & Ownership

| Command | Detailed Description |
|--------|-----------------------|
| `chmod 755 file` | Changes file permissions; 755 = owner rwx, group rx, others rx. |
| `chown user:group file` | Changes file owner and group ownership. |
| `ls -l` | Shows current permissions for each file and directory. |
| `umask` | Displays or sets default permission mask for new files/directories. |

## 👥 4. User & Group Management

| Command | Detailed Description |
|--------|-----------------------|
| `adduser username` | Creates a new user account with home directory and settings. |
| `userdel username` | Deletes a user account and optionally their home directory. |
| `usermod -aG group user` | Adds a user to a supplementary group (e.g., sudo). |
| `groupadd groupname` | Creates a new user group. |
| `groupdel groupname` | Deletes an existing group. |
| `passwd username` | Sets or changes password for a user account. |
| `id username` | Shows user ID (UID), group ID (GID), and group memberships. |

## 💽 5. Disk & File System Management

| Command | Detailed Description |
|--------|-----------------------|
| `df -h` | Shows disk usage of mounted filesystems in human-readable format. |
| `du -sh folder/` | Displays total size of a directory and its contents. |
| `mount /dev/sdX /mnt` | Mounts a disk or partition to a mount point. |
| `umount /mnt` | Unmounts a mounted filesystem safely. |
| `lsblk` | Lists block storage devices (disks and partitions). |
| `fdisk -l` | Shows partition table and disk info (use with care). |
| `mkfs.ext4 /dev/sdX` | Formats the disk or partition with ext4 filesystem. |
| `blkid` | Displays UUIDs and file system types for devices. |

## 🧠 6. Memory & Process Management

| Command | Detailed Description |
|--------|-----------------------|
| `top` | Live view of CPU, memory, and process usage in real time. |
| `htop` | Enhanced version of top with interactive UI (must be installed). |
| `ps aux` | Lists all running processes with detailed info. |
| `kill PID` | Sends termination signal to a process by its ID. |
| `killall process` | Kills all processes with a given name. |
| `nice`, `renice` | Sets or changes process priority (lower value = higher priority). |
| `free -h` | Shows RAM and swap usage in human-readable form. |

## 🌐 7. Networking Commands

| Command | Detailed Description |
|--------|-----------------------|
| `ip a` | Shows network interfaces and assigned IP addresses. |
| `ifconfig` | Legacy tool to view and configure network interfaces. |
| `ping host` | Checks connectivity and latency to another host. |
| `traceroute host` | Shows path taken by packets to reach a host. |
| `netstat -tuln` | Lists all active listening ports and services. |
| `ss -tuln` | Replacement for netstat with faster output. |
| `nmap IP` | Scans open ports and services on a target system. |
| `nslookup domain` | Checks DNS resolution of a domain name. |
| `dig domain` | Detailed DNS query tool (preferred over nslookup). |

## 🛠️ 8. Package Management

| Command | Detailed Description |
|--------|-----------------------|
| `apt update` | Updates package list (Debian/Ubuntu-based systems). |
| `apt upgrade` | Installs available updates for packages. |
| `apt install pkg` | Installs a specific package. |
| `apt remove pkg` | Removes an installed package. |
| `yum install pkg` | Installs a package on RHEL/CentOS systems. |
| `yum remove pkg` | Removes a package on RHEL/CentOS. |
| `dnf update` | Newer alternative to yum in Fedora. |
| `apt list --installed` | List all the installed packages. |
| `dpkg -l` | List all the installed packages with versions and description. |

## 🗂️ 9. Archive & Compression

| Command | Detailed Description |
|--------|-----------------------|
| `tar -cvf archive.tar dir/` | Creates tar archive from directory. |
| `tar -xvf archive.tar` | Extracts contents of a tar archive. |
| `gzip file` | Compresses file using gzip algorithm. |
| `gunzip file.gz` | Decompresses a gzipped file. |
| `zip file.zip file` | Creates zip archive. |
| `unzip file.zip` | Extracts zip file contents. |

## 🔍 10. Searching & Filtering

| Command | Detailed Description |
|--------|-----------------------|
| `grep 'pattern' file` | Searches for a text pattern in a file. |
| `grep -r 'pattern' dir/` | Recursively searches in directories. |
| `find / -name 'filename'` | Searches for files matching a pattern. |
| `locate filename` | Searches files using a prebuilt index (needs updatedb). |
| `which command` | Shows the full path of a command executable. |

## 📂 11. System Monitoring & Logs

| Command | Detailed Description |
|--------|-----------------------|
| `uptime` | Shows system uptime and load averages. |
| `dmesg` | Displays boot and hardware messages. |
| `vmstat` | Reports system performance (CPU, memory, I/O). |
| `iostat` | Shows CPU usage and disk I/O stats. |
| `journalctl` | Views logs managed by systemd. |
| `tail -f /var/log/syslog` | Monitors log file changes in real time. |
| `last` | Shows login/logout history of users. |

## 🔒 12. Permissions & Access Control

| Command | Detailed Description |
|--------|-----------------------|
| `chmod` | Sets file/directory permissions (read, write, execute). |
| `chown` | Changes file/directory ownership. |
| `umask` | Default permissions for new files/directories. |
| `sudo` | Executes command as superuser/root. |
| `su -` | Switches to another user (usually root). |

## ⌛ 13. Scheduling & Automation

| Command | Detailed Description |
|--------|-----------------------|
| `crontab -e` | Edits cron jobs for scheduling recurring tasks. |
| `crontab -l` | Lists existing cron jobs. |
| `at time` | Schedules a one-time task at a given time. |
| `systemctl` | Manages services, daemons, and system states. |
