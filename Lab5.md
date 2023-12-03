# Lab Report 5

## Student's EdStem Post
I'm having some trouble with my auto-grading script. It seems to work when all the tests pass, as it prints out "Grade: 100%". When some or all of the tests fail, I want it to print out how many tests the file had passed, formatted like "Grade: (testPassed) / (totalTests)". 
But when I run the script with a repository that contains a test file that causes some errors, it will always output "Grade: / T". I'm not sure how to fix this. I'm thinking it has something to do with a character being stored into the "totalTests" variable. Below is the output that popped up on my terminal, both it working successfully and it printing the wrong output.
<br>
(INSERT IMG HERE)
<br>
Below is my script in grade.sh
```
# set -e
CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'

rm -rf student-submission
rm -rf grading-area

mkdir grading-area

git clone $1 student-submission
echo 'Finished cloning'

testFile=`find -name ListExamples.java`

# checks if file exists
# if not, terminates bash script
if [[ -e $testFile ]] && [[ -f $testFile ]]
then 
  cp -r $testFile TestListExamples.java lib grading-area
  cd grading-area
  javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
else
  echo "File not found: ListExamples.java"
  exit 1
fi
OUTPUT=`java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples`

error=$?
if [[ $error -ne 0 ]]
then
  echo "Error Code:" $error
  echo "Error found when running tests. Please double check your code in ListExamples.java. More information is in the output.txt file."
fi

echo "$OUTPUT" > output.txt
numTests=`grep "Tests" output.txt`
totalTest=0
numFails=0
for i in $numTests
do
  if [[ ${i:0:1} > 0 ]]
  then
    if [[ $totalTest == 0 ]]
    then
      totalTest=${i:0:1}
    else
      numFails=${i:0:1}
    fi
  fi
done

if [[ $totalTest == 0 ]] && [[ $numFails == 0 ]]
then
  echo "Grade: 100%"
else
  echo "Grade:" `expr $totalTest - $numFails` / $totalTest
fi
# Draw a picture/take notes on the directory structure that's set up after
# getting to this point

# Then, add here code to compile and run, and do any post-processing of the
# tests
```
## TA's Response Post
"Hi, it looks like the problem with your script is in the if statement condition, "${i:0:1} > 0". Keep in mind that as we are traversing through the string given by numTests, each character has its own ASCII value. Say the string was "Tests passed: 1, Tests Failed: 2", when you iterate
through the string, you look at the letter "T". When we go into the if statement, since we are checking if it's greater than the integer 0, we compare the character's ASCII value, which is 54, and since 54 > 0, we enter the the if-block and we set the variable, totalTest, to "T". That's why you are
getting that output. This is also the similar case with the variable, numFails. Since we can't do subtraction on characters, it just doesn't print anything, hence the output, "Grade: /T". To fix this, I suggest using a pattern that checks to see whether the current index in the string is a digit, like 
"^[0-9]+$". Make sure you use "=~" as that lets the script now that we are checking whether the current index in the string matches the given pattern.
## Student's Takeaway
So after making the changes, the terminal now prints the correct output depending on the number of tests passed/failed. So the bug was basically that as the script was iterating through the characters in the string, it was also comparing the ASCII values of each letter as well as the digits which caused
variables, totalTests and numFails, to store characters, which ended up causing the expression "`expr $totalTest - $numFails`" and "$totalTest" to print incorrectly. To fix this bug, I just have to check whether the current character is a digit or not, which can be done by using the pattern "^[0-9]+$".
## All information needed for setup
### File and Directory Structure Needed
### Contents of grade.sh before and after fixing the bug
Before bug fix
```
# set -e
CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'

rm -rf student-submission
rm -rf grading-area

mkdir grading-area

git clone $1 student-submission
echo 'Finished cloning'

testFile=`find -name ListExamples.java`

# checks if file exists
# if not, terminates bash script
if [[ -e $testFile ]] && [[ -f $testFile ]]
then 
  cp -r $testFile TestListExamples.java lib grading-area
  cd grading-area
  javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
else
  echo "File not found: ListExamples.java"
  exit 1
fi
OUTPUT=`java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples`

error=$?
if [[ $error -ne 0 ]]
then
  echo "Error Code:" $error
  echo "Error found when running tests. Please double check your code in ListExamples.java. More information is in the output.txt file."
fi

echo "$OUTPUT" > output.txt
numTests=`grep "Tests" output.txt`
totalTest=0
numFails=0
for i in $numTests
do
  if [[ ${i:0:1} > 0 ]]  // bug occurs here
  then
    if [[ $totalTest == 0 ]]
    then
      totalTest=${i:0:1}
    else
      numFails=${i:0:1}
    fi
  fi
done

if [[ $totalTest == 0 ]] && [[ $numFails == 0 ]]
then
  echo "Grade: 100%"
else
  echo "Grade:" `expr $totalTest - $numFails` / $totalTest
fi
# Draw a picture/take notes on the directory structure that's set up after
# getting to this point

# Then, add here code to compile and run, and do any post-processing of the
# tests
```
After bug fix
```
# set -e
CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'

rm -rf student-submission
rm -rf grading-area

mkdir grading-area

git clone $1 student-submission
echo 'Finished cloning'

testFile=`find -name ListExamples.java`

# checks if file exists
# if not, terminates bash script
if [[ -e $testFile ]] && [[ -f $testFile ]]
then 
  cp -r $testFile TestListExamples.java lib grading-area
  cd grading-area
  javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
else
  echo "File not found: ListExamples.java"
  exit 1
fi
OUTPUT=`java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples`

error=$?
if [[ $error -ne 0 ]]
then
  echo "Error Code:" $error
  echo "Error found when running tests. Please double check your code in ListExamples.java. More information is in the output.txt file."
fi

echo "$OUTPUT" > output.txt
numTests=`grep "Tests" output.txt`
totalTest=0
numFails=0
for i in $numTests
do
  if [[ ${i:0:1} =~ ^[0-9]+$ ]]  // bug fix here
  then
    if [[ $totalTest == 0 ]]
    then
      totalTest=${i:0:1}
    else
      numFails=${i:0:1}
    fi
  fi
done

if [[ $totalTest == 0 ]] && [[ $numFails == 0 ]]
then
  echo "Grade: 100%"
else
  echo "Grade:" `expr $totalTest - $numFails` / $totalTest
fi
# Draw a picture/take notes on the directory structure that's set up after
# getting to this point

# Then, add here code to compile and run, and do any post-processing of the
# tests
```
### Full command line to trigger the bug
Within the list-examples-grader directory:
```
bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-lab3
```
where the repository can be any valid lab3 repository that contains tests that fail.
### Description to fix bug
To fix the bug, instead of comparing each individual indices with the integer 0, which causes the script to just compare ASCII values, you have to change it so that it tests to see whether the character follows the pattern, "^[0-9]+$", which checks to see whether the character is a digit or not. When
implementing this, the character at the current index is a digit, then we can update the variables totalTest and numFails correctly, if it's not a digit, then we just move onto the next index in the string.
