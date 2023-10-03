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
Before the cd command was run, the current working directory was "/home/lecture1". When the cd command was run with a directory, it successfully changed the working directory to the selected directory, which in this case was "/home/lecture1/messages". If the code block below was run however, there would be an error.
```
[user@sahara ~]$ cd messages
bash: cd: messages: No such file or directory
```
This is because of the filesystem and how it was structured. The current working directory was the root directory "/home". When running the cd command, it threw an error because the terminal does not know where the folder "messages" is. This is because in the filesystem, the folder "messages" is contained within the folder "lecture1". So we can conclude that from the root working directory, "messages" is not considered as a directory, but from the lecture1 working directory, it is.

**3. Using cd with a file**

---
## Using ls
