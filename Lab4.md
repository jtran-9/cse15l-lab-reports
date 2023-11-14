# Lab Report 4

## Step 4 - Log into ieng6
![login](https://i.imgur.com/mWSzr3b.png)
Keys pressed:
```
s s h <CTRL C> <CTRL V> @ i e n g 6 . u c s d . e d u
```
I had my CSE15L specific username on a separate tab and copy pasted it into the terminal while logging into my ieng6 account.


## Step 5 - Clone your fork of the repository from your Github account (using the SSH URL)
![clone](https://i.imgur.com/TY29FVU.png)
Keys pressed:
```
g i t <SPACE> c l o n e <SPACE> <CTRL C> <CTRL V> <ENTER>
```
The SSH url was already opened in my github account on another tab so I just copy pasted the URL into the command line.


## Step 6 - Run the tests, demonstrating that they fail
![run failed tests](https://i.imgur.com/jVA2NGq.png)
Keys pressed:
```
c d <SPACE> l <TAB> <ENTER>
b a s h <SPACE> t <TAB> <ENTER>
```
I used tab to autofill the names of both the directory, "lab7" and the bash script "test.sh".


## Step 7 - Edit the code file ListExamples.java to fix the failing test 
![command line](https://i.imgur.com/ZLaedCV.png)
![edit file](https://i.imgur.com/H2Owo5r.png)
Keys pressed:
```
v i m <SPACE> L i <TAB> . j a v a <ENTER>
x i 2 <ESC>
: w q <ENTER>
```
I used tab to autofill the name "ListExamples" and filled in the file extension ".java". When entering vim, my cursor was already on the character I needed to delete so I used the operator 'x' to delete the current character, then used the operator 'i' to enter INSERT MODE and typed '2' to change the variable name. I then pressed the ESC key to exit INSERT MODE to go into NORMAL mode. Finally, I saved my changes by typing ":wq".


## Step 8 - Run the tests, demonstrating that they now succeed
![run successful tests](https://i.imgur.com/zqg7B2r.png)
Keys pressed:
```
<UP> <UP> <ENTER>
```
The command "bash test.sh" was 2 commands up the command history, so I used the arrow keys to access it and run the tests.


## Step 9 - Commit and push the resulting change to your Github account
![commit and push changes](https://i.imgur.com/oMAu1qZ.png)
Keys pressed:
```
g i t <SPACE> a d d <SPACE> . <ENTER>
g i t <SPACE> c o m <TAB> <ENTER>
i B u g <SPACE> f i x e s <ESC>
: w q <ENTER>
g i t <SPACE> p u s h <ENTER>
```
I used git add and git commit to choose the changes that I want to push to the main branch. I used TAB to autofill some keywords. When I did "git commit", I used 'i' to go into INSERT MODE and typed "Bug fixes" as my changes and pressed ESC and ":wq" to save and exit vim. I then pushed my changes to the main branch.


## Changes on Github
![repository](https://i.imgur.com/4f5dxF4.png)
![file contents](https://i.imgur.com/JKdFh4Q.png)
As you can see, the changes I made in the terminal from vim were updated to the fork on my repository.
