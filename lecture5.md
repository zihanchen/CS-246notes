#Lecture 5

##Variables (continue)

- Double quotes allow variables to expand to their values, whereas single quotes do not
- Both kinds of quotes supress expansion of globbing patterns  

##Source-code Management

####Source-code management software can help
- track changes to software code (program files) overtime
- backout of changes 
- maintain multiple versions(branches)
- provide a mechanism for multiple developers to work on the same code base simultaneously
- shared access to the same physical file is dangerous
- merging changes from different developers can be tricky  

>How does Git work?  
>Git is a ditributed version control system  
>- git clone: get a local copy of a remote repository  
>- git pull: get latest changes from the rermote repository  

##Shell Scripting  
A shell script is a file that contains sequences of Linux commands, executed as a program.  
  
An example
```bash
$> cat basic
#!/bin/bash #<-- this is the shell you choose
date
whoami
pwd
$> bash basic
Tue 19 May 2015 12:06:36 EDT
present
/Users/present/Desktop/notes/shell/example #it will be executed in bash
```
If the execute bit is on, we can also just do this:
```bash
$> ./basic
```
####Command Line Arguments

$1,$2...  
$0: The name of the program

#####Example 1
Check whether a word is in the decionary(in `/usr/share/dict/words`)  
```bash
egrep "^$1$" /usr/share/dict/words
```
so the script looks like  
```bash
#!/bin/bash
egrep "^$1$" /usr/share/dict/words
```
and we can execute it (if its name is goodPassword)
```bash
$> ./goodPassword
```  
Every program returns a status code when finished\\
In Unix, 0 is success and other is failure

so we can improve our script to:
```bash
#!/bin/bash

usage(){
	echo "Usage: $0 password"
	# $0 - name of program
	exit 1
}

# $# - number of arguments 
if [ $# -ne 1 ]; then
	usage
fi

egrep "^$1$" /usr/share/dict/words > /dev/null

# $? - status of most recently executed command

if [ $? -eq 0 ]; then
	echo "Not a good password"
else
	echo "Maybe a good password"
fi
```
- # denotes a comment
- Often we want to make sure an exact number of arguments is provided and if\\
not provide a usage message
- Usage message is commonly isolated into its own function

######The general form of if statement  
```bash
if [ condition ];then #note whitespace around condition is important
	...
elif [ condition ];then
	...
...
```

####Example 2  
Loop through and print numbers from 1 to $1
```bash
#!/bin/bash
#count limit ----- counts the numbers from 1 to limit

unsage() {
	echo "Usage: $0 limit" 1>&2
	echo " where limits is at list 1" 1>&2
	exit 1
}

if [ $# -ne 1]; then 
	usage
fi

if [ $1 -lt 1 ]; then
	usage
fi

x=1
while [ $x -le $1 ]; do
	echo $x
	x=$((x + 1)) #arithmetic
done
```  
Suppose we want to loop over a list
####Example 3
Rename all .cpp files in current direcotry to .cc files
```bash
#!/bin/bash

for name in *.cpp; do # use a glob
	mv ${name} ${name%cpp}cc
done
```

####For loop
- for ... in __ ;do... : set the given variable to each word in a given list
- ${name%app}: value of $name without trailing cpp
- eample:How many times does word $1 occur in file $2

```bash
#!/bin/bash

x=0
for word in	`cat $2`; do
	if [ $word = $1 ] then
		x=$((x + 1))
	fi
done
echo $x
```

####Example 
Payday is the last Friday of the month. When is this monts payday?
```bash
#!/bin/bash

answer(){ # $1, $2 are function's parameters
	if [ $1 -eq 31 ]; then
		echo "This month: on the ${1}st"
	else
		echo "This month: on the ${1}th"
	fi
done
```






 
