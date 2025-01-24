1. Semicolon
- To put 2 or more commands in same line. Execution will be sequential.

![image](https://github.com/user-attachments/assets/3ec0df44-a6d6-4e98-a020-c9309aeafd33)

2. Ampersand
- When line ends with &, shell will not end for command to finish. We'll get our shell prompt back and command is executed in background.After execution, we get message

![image](https://github.com/user-attachments/assets/55c52092-df47-43a7-b685-e5eefd2cc771)

3. Dollar Question mark ($?)
- Exit code of previous command is stored in $?.
- 0 means success, 1 means fail

![image](https://github.com/user-attachments/assets/f5c72c9e-0fd0-4a47-b2b7-9d4b4dadbde3)

4. Double ampersand (&&)
- It is logical AND. Second command gets executed only if first one succeeds (returns zero exit status)

![image](https://github.com/user-attachments/assets/508123cd-5c36-4368-afa7-1d9721a364d8)

5. Double vertical bar (||)
- It is logical OR. Second is executed only if first one fails

![image](https://github.com/user-attachments/assets/341c7a7c-020d-40f0-a333-1e035cfc10a8)

6. Pound (#)
- To write shell comments

7. Escaping special characters
- \ (backslash) enables use of control characters
- End of line backslash :- lines ending with backslash are continued on next line

![image](https://github.com/user-attachments/assets/6ee46fa8-3f52-4b0b-aa24-8b841920739d)
![image](https://github.com/user-attachments/assets/ea8e8087-77d3-4b99-b09d-9c111594df08)


-
