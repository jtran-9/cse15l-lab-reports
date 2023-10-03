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
Before the cd command was run, the current working directory was "/home/lecture1". When the cd command was run with a directory, it successfully changed the working directory to the selected directory, which in this case was "/home/lecture1/messages". This does not throw an error. But if the code block below was run however, there would be an error.
```
[user@sahara ~]$ cd messages
bash: cd: messages: No such file or directory
```
This is because of the filesystem and how it was structured. The current working directory was the root directory "/home". When running the cd command, it threw an error because the terminal does not know where the folder "messages" is. This is because in the filesystem, the folder "messages" is contained within the folder "lecture1". So we can conclude that from the root working directory, "messages" is not considered as a directory, but from the lecture1 working directory, it is.

**3. Using cd with a file**
```
[user@sahara ~]$ cd Hello.java
bash: cd: Hello.java: No such file or directory
```
Before running the command, the working directory was the root directory. When trying to run the cd command with a file, it threw an error. Even though "Hello.java" can be seen from the current working directory, it is not considered as a directory, as a directory can be defined as a "folder that is not contained in any other folder as seen from the current working directory". In other words, the folder has to be on the same level as the directory.

---
## Using ls
**1. Using ls with no arguments**
```
[user@sahara ~/lecture1]$ ls
Hello.class  Hello.java  messages  README
```
Before running the ls command, the current working directory was "/home/lecture1". When running ls with this working directory, it printed out all the files and folders that were currently visible to the current working directory. In other words, it printed out all the things contained inside the "lecture1" folder. This command does not throw an error. This means that for the ls command, running it with no argument just prints everything in the current working directory.

**2. Using ls with a directory**
```
[user@sahara ~/lecture1]$ ls messages
en-us.txt  es-mx.txt  ko.txt  zh-cn.txt
```
Before running the command, the current working directory was "/home/lecture1". When running the ls command with the directory "messages", it ended up printed all the contents contained in the "messages" folder. This means that using ls on a directory prints out all the files and folders contained in that selected directory, if it exists. In addition, there was no error that had occurred.

**3. Using ls with a file**
```
[user@sahara ~/lecture1]$ ls Hello.java
Hello.java
```
The working directory was "/home/lecture1" before the command was run. When running the ls command with a file contained within the current working directory, it just printed out the file name. This is probably because the argument was not a directory, so it doesn't contain any other files or folders. Since it is a file, the ls command just prints out the file name itself. This does not throw an error.

But if the file is not contained within the current working directory, like the code block below tries to do, it will throw an error as the system cannot identify where the file is located.
```
[user@sahara ~/lecture1]$ ls en-us.txt
ls: cannot access 'en-us.txt': No such file or directory
```

---
## Using cat
**1. Using cat with no arguments**
