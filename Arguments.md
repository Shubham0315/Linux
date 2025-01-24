- Shell performs command line scan. It scans the command line and cut it to arguments

1. White Space Removal
- Parts separated by one or more spaces are considered as separate arguments. First argument us command and other arguments are given to command

![image](https://github.com/user-attachments/assets/5f827d01-60d2-40b4-8f57-22b44cfcadb7)

2. Single Quotes
- We can prevent removal of white spaces by quoting spaces. Contents of quoted string are considered as one argument

![image](https://github.com/user-attachments/assets/c3019ca7-a70f-4d9b-b6fb-57490077324b)

3. Double Quotes
- We can prevent removal of white spaces by double quoting spaces.

![image](https://github.com/user-attachments/assets/eef4d98e-cc47-42d1-a1ff-4f741efd67ee)

4. echo and quotes
- Quoted lines can include escaped characters recognised by echo command.
- \n for newline and \t for tab (8 white spaces)

![image](https://github.com/user-attachments/assets/b141d480-32e2-44ed-b8f5-7df6d1903e7c)

5. Command type
- Some are external, some are builtin for shell. External are programs with their own binary and are located in /bin or /sbin.
- Builtin are part of shell program itself
- We can use "type $command" to check the type
- Using this type, we can also see if command is aliased or not
- Some commands are builtin as well as external. Here builtin version takes priority. To run external version, we've to give full path of command

![image](https://github.com/user-attachments/assets/9ca6c804-685e-43a2-b29e-8a93f83dee52)

- "which" command will search binaries in $PATH env variables

![image](https://github.com/user-attachments/assets/706c3116-400d-446b-85b6-b5b3e041245a)

6. Aliases
- Shell allows to create aliases to create easier name to remember for existing command
- To view aliases:- alias c ll
- To unalias :- unalias $Command

![image](https://github.com/user-attachments/assets/13ec4f3d-4920-4dc1-a00f-08c32d15d251)
![image](https://github.com/user-attachments/assets/5d75f07f-3aba-47bb-a8f3-f0cd8addb37c)

7. Dispaly shell expansion
- We can display shell expansion with set-x and stop displaying with set+x






