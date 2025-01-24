![image](https://github.com/user-attachments/assets/4de49347-1b3d-4e5a-91cf-7212869f17a4)- Commands that are used with pipe are often called filters. They can be used as building blocks

1. cat
- When between 2 pipes, cat command does nothing except putting stdin on stdout)

2. tee
- tee filter puts stdin on stdout and also into a file.

3. grep
- To filter lines of text containing certain string. Use -i for case insensitiveness
- grep -v outputs lines not matching the string
- grep -A1 for dispalying one line after result
- grep -B1 for displaying one line before result
- grep -C1 to dispaly one line before and after of string

![image](https://github.com/user-attachments/assets/3b6fd411-c28e-4ce9-bfd3-39aab7aa874c)

4. cut
- Can select columns from files, depending on delimeter or count of bytes

![image](https://github.com/user-attachments/assets/29284be9-ee31-4b6a-9e5f-54c909c998e0)

5. tr
- To translate characters.
- tr -s :- used to squeeze multiple occurences of character to one
- tr -d :- to delete characters

![image](https://github.com/user-attachments/assets/121d7473-b15e-4522-81ef-4b817053a107)

![image](https://github.com/user-attachments/assets/1231fea1-2733-4c00-9e07-c85819e69c80)

6. wc
- To count words, lines, characters

![image](https://github.com/user-attachments/assets/a672882c-04e2-4654-98f7-fee1ed809629)

7. sort
- To filter out in alphabetical order

8. uniq
- To remove duplicates from sorted list

![image](https://github.com/user-attachments/assets/a2d85fe3-6f5f-4bc5-85d9-9fd5290b339b)

9. sed
- Stream Editor :- to perform editing functions in stream using regular expressions
- Add g for global replacements (all occurences of string per line)

![image](https://github.com/user-attachments/assets/a50de6b4-9d08-460d-b78d-4685af46368b)






