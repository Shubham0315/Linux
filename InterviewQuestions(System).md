What is the difference between soft link and hard link?
-
- Soft link is a pointer or shortcut to another file or directory.
  - It points to file name not actual data
  - If original file is deleted. soft link is broken
  - Command :- **ln -s $file $Link_name**
  -         :- ln -s /home/user/file.txt shortcut.txt
 
- Hard link is another name for the same file data (inode) on the disk
  - Points directly to inode (data) of the file
  - If original file is deleted, data still exists via hard link
  - Command :- ln $file $link_name
  -         :- ln file.txt hardlink.txt
  - Both file.txt and hardlink.txt has same data

-----------------------------------------------------------------------------------

What are some common Linux file systems?
-
- ext4, ext3, ext2, XFS, Btrfs, ZFS
- ext4 is most stable and de3fault in linux
- XFS is for high performance

-----------------------------------------------------------------------------------

How to setup cronjob in linux?
-
- To edit cronjobs for current user :- **crontab -e**
- To list cronjobs :- **crontab -l**
- Cron Syntax :- * * * * *
  - Minute (0-59)
  - Hour (0-23)
  - Day of month (1-31)
  - Month (1-12)
  - Day of week (0-7)
 
- Run script every day at 2AM :- 0 2 * * *
- Run command every 5 mins :- */5 * * * *

-----------------------------------------------------------------------------------

How to run cron at every second?
-
- Cron cannot be run every second, it has minimum resolution of 1 min

- To run cron every second or setup as such
  - Use while loop inside script
  -     #!/bin/bash
  -     for i in {1..60}
  -     do
  -       echo "Running task at $(date)"
  -       sleep 1
  -     done
 
- We can also use sleep command while executing a script giving time as 1 sec :- **sleep 1 script.sh**

- We can also use watch command
  - Command :- **watch -n 1 script.sh**

-----------------------------------------------------------------------------------

How to debug script in linux?
-
- Use "set" for debugging
- Add below at top of script
  - **set -x** :- prints commands and their arguments as they're executed
  - **set -e** :- exit immediately if command exits with non zero status
 
- Or we can run script with :- **bash -x script.sh**
  - This will show line by line execution with expanded variables

-----------------------------------------------------------------------------------
 
How do you check which ports are open on a Linux server?
- 
- Using ss :- ss -tuln
  - -t for TCP, -u for udp, -l for listening sockets
 
- Using netstat. Install netstat using :- **sudo yum install net-tools**

- Using lsof. To list open files including network connections
  - Command :- sudo lsof -i -P -n | grep LISTEN
 
-----------------------------------------------------------------------------------

How do you find disk usage of a directory?
- 
- Use du command to get disk usage of specific directory
  - Command :- **du -hs $directory**

- To check disk usage for entire filesystem
  - Command :- **df -h**
 
-----------------------------------------------------------------------------------

How do you monitor real-time logs in Linux?
-
- Using tail -f :- To view end of file, -f allows to follow the log file as it updates in real time
- less :- To scroll back through file
- Using watch to periodically check log file and execute command every few seconds :- **watch tail -n 10 $file**
- Using jornalctl :- If our system uses systemd, logs are stored in journal and we can use journalctl to monitor in real time
  - Command :- **journalctl -f**

-----------------------------------------------------------------------------------

How to find top memory-consuming processes?
- 
- Using top command
  - It displays system resource usage in real time, including memory consumption
 
- Using ps command
  - ps (process status) command is versatile way to display process information. Use below to find top memory consuming processes
  - Command :- **ps aux --sort=-%mem | head -n 10**
 
- Use free command
  - Provides snapshot of total, used and free memory in system
  - Command :- **free -h**

-----------------------------------------------------------------------------------

How do you manage services with systemd?
-
- Systemd is a default system and service manager for many linux distros.

- To start service :- **sudo systemctl start nginx**
- To stop service :- **sudo systemctl stop nginx**
- To restart service :- **sudo systemctl restart nginx**
- To enable service :- **sudo systemctl enable nginx**
- To check status :- **sudo systemctl status nginx**
- To check if service is enabled :- **sudo systemctl is-enabled nginx**
- To check logs of service :- **sudo jorunalctl -u nginx**

-----------------------------------------------------------------------------------

How to find which process is using a specific port?
-
- **lsof -i :8080** :- list process using specific port
- **netstat -tunlp | grep :8080** :- shows PID and process using port
- **fuser PORT/tcp** :- provides PID of process using port

-----------------------------------------------------------------------------------

How would you secure a Linux server?
- Keep system up to date. Regularly install system and ensure latest patches are installed :- **sudo yum update**
- Use firewall to control incoming and outgoing traffic based on defined security rules
- Secure SSH access using SSH keys. Copy public key to server
- Disable unnecessary services :- **sudo systemctl stop service**

-----------------------------------------------------------------------------------

How do you manage user permissions and groups?
-
- To create new user :- sudo useradd username
- To add new group :- sudo groupadd groupname
- To add user to a group :- sudo usermod -aG groupname username    (-aG for append group with user)
- To manage permissions :- chmod
- To change file ownership :- sudo chown owner:group filename     (to change onwer and group of file)

-----------------------------------------------------------------------------------

How do you handle log rotation?
-
- Log rotation is the process of managing log files by ayto rotating, compressing, removing or mailing them to ensure log files dont consume too much disk space
- Logrotate :- Commonly used in linux

- Logrotate typically runs cron, daily or weekly, to rotate logs based on pre-configured policies
- Main config file is :- **/etc/logrotate.conf**

- To manually trigger log rotation :- **sudo logrotate /etc/logrotate.conf**
- Logrotate cron job path :- **/etc/cron.daily/logrotate**

-----------------------------------------------------------------------------------

