# Lab Report 1
## Workspace Structure For Reference
![Image](https://i.imgur.com/qYmLMqx.png)

---
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
It will only work when you include its path.
```
[user@sahara ~/lecture1]$ ls messages/en-us.txt
messages/en-us.txt
```

---
## Using cat
**1. Using cat with no arguments**
```
[user@sahara ~]$ cat
lecture1
lecture1
It prints out my entire sentence.
It prints out my entire sentence.
```
Before the command was run, the working directory was the root directory, "/home". Surprisingly, running cat with no arguments did not throw an error. Instead, it waited for user input and then just printed out what was just typed in. This means that to the cat command, having no arguments just tells it that it should wait for some user input and then it will print out that input after the user finishes entering it.

**2. Using cat with a directory**
```
[user@sahara ~/lecture1]$ cat messages
cat: messages: Is a directory
```
Before the command was run, the working directory was "/home/lecture1". The terminal outputted the error message "messages: Is a directory". This error popped up because a directory was placed as its argument and the cat command is used for printing out the contents of a file. A directory could contain more folders and files so by putting a directory as an argument, we're not specifying which file should be read and printed out to the terminal.

**3. Using cat with a file**
```
[user@sahara ~/lecture1]$ cat Hello.java
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;

public class Hello {
  public static void main(String[] args) throws IOException {
    String content = Files.readString(Path.of(args[0]), StandardCharsets.UTF_8);    
    System.out.println(content);
  }
}[user@sahara ~/lecture1]$ 
```
Before the command was run, the working directory was "/home/lecture1". When running the command with a file, there was no error, it simply prints out the contents of the file. This makes sense since the whole point of the cat command is to print the contents of file(s). 
```
[user@sahara ~/lecture1]$ cat messages/ko.txt
안녕하세요 세계
```
This command also works when you put in specific paths to files as the argument.
