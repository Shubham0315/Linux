1. stdin, stdout and stderr
- Bash shell has 3 basic streams, it takes input from stdin (Stream 0), it sends output to stdout (stream 1) and it sends error messages to stderr (stream 2)
- Keyboards us stdin whereas stdout/stderr both go to display

![image](https://github.com/user-attachments/assets/62b71143-6940-4d06-a722-f165926c3263)

2. Output redirection
- > stdout :- can be redirected with greater than sign. While scanning line, the shell will see > sign and will clear the file

<img width="774" alt="image" src="https://github.com/user-attachments/assets/f387291e-6f2a-41e3-8679-30aaac849223" />

- >> append :- to append output to file

![image](https://github.com/user-attachments/assets/7c1ffae9-06d2-49b3-adc1-d9254fa71373)

3. Error redirection
- 2> stderr :- Useful to prevent error messages from cluttering screen

![image](https://github.com/user-attachments/assets/3cdf7fb7-f40e-4142-958d-0403086604a6)

- 2>&1 :- to redirect both stdout and stderr to same file

4. Input redirection
- Redirecting stdin is done with <


