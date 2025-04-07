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

What is the difference between grep and egrep?
-
- grep is used for searching and filtering text based on patterns
- egrep is grep -E, which supports extended regex. Extended regex allow more complex patterns without needing to escape special characters

-----------------------------------------------------------------------------------

How would you find a file in Linux?
-
- Using find command. Used to search files and directories based on name, size, type
- Command :- **find -name file**
- Find by type :- **find . -type f/d/l**   (file/dir/links)
- Find by extension :- **find . -name *.txt**
- Find by size :- **find . -size +100M**
- Find by time :- **find . -mtime -7**    (modified last 7 days)

-----------------------------------------------------------------------------------

What is ps command and what does it do?
-
- Process status
- To display info about active processed running on system
- Provides details such as PID, terminal associated with process, CPU, memory usage
- ps -ef

-----------------------------------------------------------------------------------

How would you check the available memory on a Linux system?
-
- free command :- to check memory usage. Gives total, used, free, shared, available memory columns
- top command :- provides real time CPU,memory usage and more

-----------------------------------------------------------------------------------

Explain the kill command and its options.
-
- kill command is used to send signal to process for terminating it.
- kill sends TERM signal (signal no 15) which asked the process to terminate
- To forcefull terminate process :- **kill -9 PID**
- killall :- Instead of using PID we can use name of process to terminate all instances of process

-----------------------------------------------------------------------------------

What is awk used for?
-
- awk is used for pattern scanning and processing. Used to manipulate and analyse data in files
- It allows to perform operations like searching, extracting, formatting and transforming data from structured text

-----------------------------------------------------------------------------------

What is the difference between > and >> in Linux?
-
- > overwrite output in existing file. If file is not there, it created one
  - echo "hello" > example.txt
 
- >> Append output at the end of file without overwriting existing content. If file doesnt exist, creates new one
  - echo "hello" >> example.txt
 
- 2> To overwrite error output :- **command 2> error.log**
- 2>> to append error output :- **command 2> error.log**

-----------------------------------------------------------------------------------

What is a shell? What are the types of shells in Linux?
-
- Shell us a CLI that allows users to interact with OS. It acts as bridge between user and kernel, interpreting commands typed by user and executing them.
- It takes user input, interprets and passes it to OS, displays the result
- Types of shell :- Bash, sh, ksh, zsh
- Bash :- Bourne again shell. Most common for linux. Supports scripting, variables, loops  (/bin/bash)
- sh :- original unix shell, less feature than bash  (/bin/sh)

- To find current shell :- **echo $SHELL** or **cat /etc/shells**

-----------------------------------------------------------------------------------

What are positional parameters in a shell script?
-
- These are variables that hold arguments passed to script when it is executed. These parameters allow us to access input values directly inside our script.
  - e.g :- ./script.sh arg1 arg2 arg3
  - In script $0 is script name (./script.sh), $1 is arg1, $2 is arg2, $3 is arg3
  - To check no of parameters inside script :- $#
  - To quote all arguments individually :- $@
  - To quote all arguments  as single string :- $*
 
-----------------------------------------------------------------------------------

What is the difference between = and == in shell scripting?
-
- = is used in [] or [[]]. It compares strings for equality
- == is used in [[]] only. It also compares strings for equality

-----------------------------------------------------------------------------------

How do you read input from a user in a shell script?
-
- We can read user input in shell script using read command. It waits for user to type something and stores the input into a variable
  - e.g :- read variable
-     echo "What is your name?"
      read name
      echo "Hello, $name!"
- This will prompt :- What is your name?
  - Here we need to provide input
 
- Custom Prompt
  - read -p "Enter your age: " age
  - echo "You are $age years old"
 
- To hide something like password :- read -s (hides what we type)

-----------------------------------------------------------------------------------

What does #!/bin/bash mean?
-
- It is called shebang which lies at top of shell script
- #! tells system what follows is the path to interpreter that should be used to run script
- /bin/bash is absolute path to bash shell
- So this line means use the bash shell to interpret and run script
- If we dont specify the shell, script might break with errors or behave unexpectedly

-----------------------------------------------------------------------------------

How do you use if, else, elif conditions in shell scripts?
- 
- 
