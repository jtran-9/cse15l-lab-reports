# Lab Report 1

## Using cd
**1. Using cd with no arguments**
```
[user@sahara ~/lecture1]$ cd
[user@sahara ~]$ cd
```
In the first run of the cd command, the current working directory was "/home/lecture1". When run with no arguments, it changes the working directory to the root directory. To prove these changes, I ran the code block below: 
```
[user@sahara ~/lecture1/messages]$ cd
[user@sahara ~]$ 
```
I changed the work directory to "/home/lecture1/messages", which is two levels down from the root. When cd was run with no arguments, it changed the working directory back to the root directory. In addition, there was no error that occurred when this command was run. In conclusion, running cd with no arguments changed the working directory to the default root directory.

**2. Using cd with a directory**
```
[user@sahara ~/lecture1]$ cd messages
[user@sahara ~/lecture1/messages]$ 
```
Before the cd command was run, the current working directory was "/home/lecture1". When the cd command was run with a directory, it successfully changed the working directory to the selected directory, which in this case was "/home/lecture1/messages".

**3. Using cd with a file**

---
## Using ls
