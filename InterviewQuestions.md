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
-
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
- if, else, elif statements in shell scripting let us make decisions based on conditions.

![image](https://github.com/user-attachments/assets/c0027eae-e33c-4e6e-8819-222918219054)

- We can use comparison operators like :- -eq, -ne, -ge, -le, -lt, -gt or =, !=,   

-----------------------------------------------------------------------------------

What is the use of case statements in shell scripts?
-
- Case statement is used to handle multiple conditions more cleanly than using many if, elif, else blocks
- It is cleaner and easier to read when we have many possible values to check

![image](https://github.com/user-attachments/assets/68a03f10-8deb-4335-b093-b6430e6878c8)

- ;; ends each pattern block
- * is like elase
- esac ends the case

- Use case over if when
  - We're checking single variable against multiple possible values
  - We want to keep code more reliable
 
-----------------------------------------------------------------------------------

How do you use loops (for, while, until) in shell scripting?
-
- Loops are used in shell scripting to repear block of code multiple times, depending on condition or a fixed number of iterations.
- For Loop
  - Used when we want to iterate over fixed set of values such as list or range of numbers
 
![image](https://github.com/user-attachments/assets/203f84eb-12fa-44b0-b53e-12e23752c391)

- While Loop
  - Continues executing as long as conditions remain true

![image](https://github.com/user-attachments/assets/01a58b17-5e31-493b-82f0-9ff98fb6e601)

- Until Loop
  - It continues executing as long as condition is false

![image](https://github.com/user-attachments/assets/1cc51a34-cc44-4774-b7b8-bbde0f2f13ad)

-----------------------------------------------------------------------------------

What is the difference between break and continue?
-
- Both break and continue are used to control flow of loops (like for, while, until)
- Break
  - Break statement is used to exit loop completely, regardless of whether loop condition is true or not
  - It terminates entire loop and execution moves to next line of code after loop
 
![image](https://github.com/user-attachments/assets/43529987-f223-49ca-90e0-564efd06f2b2)

- Continue
  - Used to skip current iteration of loop and move to next iteration
  - It only skips rest of the current loop cycle and continues with next iteration of loop

![image](https://github.com/user-attachments/assets/05004ef0-4b50-4306-9a45-b6d7e268b678)

-----------------------------------------------------------------------------------

How do you handle command-line arguments in shell scripts?
-
- Handling command line arguments in shell scripts allows users to pass input values when running script, which can then be used in script's logic
- We can handle them using positional parameters ($0, $1, $2, $@, $#)
- While running script we can do :- **./script.sh arg1 arg2**

-----------------------------------------------------------------------------------

How do you redirect input and output in shell scripting?
-
- In shell scripting, we can redirect input and output to/from files or other streams, which is powerful feature that lets you control how data flows in and out of commands
- To redirect std output to a file (overwrite a file) :- > :- echo "This is a test" > output.txt
- To redirect standard output to file (Append file) :- >> :- echo "Adding more text" >> output.txt

- To redirect std input from file :- < :- cat < input.txt
  - Takes content from input.txt and passed to cat command
 
- To redirect std error to file (overwrite) :- 2> :- cat non_existent_file 2> error.log
- To redirect std error to file (append) :- 2>>

- We can also use pipes

-----------------------------------------------------------------------------------

What are some commonly used string operations in shell scripts?
-
- String operators are essential for manipulating and working with text data.
- To get length of string :- ${#variable}
- To replace string :- ${string/old/new)
- String comparison :- ==, =!, <, > [[]]
- To convert to uppercase :- ${string^^}
- To convert to lowercase :- ${string,,}

-----------------------------------------------------------------------------------

How do you manage errors and exit codes in shell scripting?
-
- In shell scripting, error handling and exit codes are crucial for determining whether a script or command has executed and for managing flow of execution based on success or failure
- Every command in shell script return exit code or status to indicate whether command is success or not
  - Exit code 0 :- Success with no error
  - Non-zero exit code :- Command failed
  - 1 :- command failed
  - 2 :- Misuse of shell bulletins
 
- Use $? to capture exit status and store it
- Use set -e to exit on errors immediately.
- Use set -u to handle undefined variables

-----------------------------------------------------------------------------------

What is set -e, set -x, set -u ?
-
- Set is  uilt in command used to control behaviour of shell
- set -e :- exit on error, if command gives non zero exit status. In production scripts where you need to ensure that errors do not go unnoticed.
- set -x :- to enable debugging, shell will print each command and its arguments as they're executed
- set -u :- treat undefined variables as error. Script will exit immediately if any variable is used without being defined. This prevents issues caused by accidental typos or uninitialized variables and ensures that all variables are explicitly defined before being used

-----------------------------------------------------------------------------------

How do you check the memory or disk usage using shell scripting?
-
- To check memory usage :- free
- To check disk usage :- df or du
- To monitor memory usage :- top
- To monitor memeory and disk usage :- ps

-----------------------------------------------------------------------------------

How would you monitor a log file in real-time and trigger an alert?
-
- 


-----------------------------------------------------------------------------------

Explain awk command
-
- AWK is powerful scripting language and command line tool used for text processing and data extraction in Unix env
- Columns content are fileds for awk, awk will scan each line in file and give us required output
- Syntax :- **awk 'pattern { action }' input_file**
  - Pattern :- condition determining when action to be executed
  - action :- what to do when pattern matches
  - input_file :- file on which awk to perform action
 
- awk divides each input line into fields
  - $0 :- entire line
  - NF :- no of fields in current record
  - NR :- no of records processed
 
- print entire line :- awk '{ print $0 }' file.txt
- print specific fields :- awk '{ print $1, $2 }' file.txt

-----------------------------------------------------------------------------------

Explain grep command
-
- grep is used to search patterns in files or input provided to it
- It stands for global regular expression print
- It allows to search through files for specific text and print matching lines
- Syntax :- **grep "pattern" file.txt**
- To display line numbers with matches :- grep -n "pattern" file.txt
- To count number of matches :- grep -c "pattern" file.txt
- To serach multiple patterns :- grep -E "p1|p2" file.txt

-----------------------------------------------------------------------------------

Explain sed command
-
- stream editor
- Powerful linux tool used for text manipulation.
- Used to perform basic text transformations on inout stream. Basically to search and replace
- Syntax :- **sed [OPTION] 'command' file.txt**

- To search pattern and replace :- sed 's/word'replace/' file.txt
- To replace all occurences in each line :- **sed 's/word/replace/g' file.txt**

-----------------------------------------------------------------------------------

/dev/null
-
&>/dev/null: Redirects both standard output and error to /dev/null, so it doesn’t print anything to the terminal
