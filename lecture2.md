#Lecture 2

##File System & Globbing Pipes

###Linux File System
"Ordinary" files: mp3s, programs  
Directories: files that contain other files 

```
					/(root)
		/      |       |         \
	  bin     etc     home       usr
	/    \     |       |         /  \
  bash   ls   shell  nanaeem    bin include(c/c++ header files)
					 /   \
				  cs241  cs246
```

Path: specify the location of any file in the file system  
Absolute Path: a path that starts at the root directory  
```bash
$> /home/nanaeem/cs246
```
Current Directory: the directory you are "sitting" in  
```bash
$> pwd (present working directory)
``` 

Relative Path: specify a file loaction relative to the current directory  
For example, your pwd is  
```bash
/home/nanaeem
```
and you want to go to
```bash
/home/nanaeem/cs245/a0
```
so the relative path is 
```bash
cs245/a0
```
To change the directory you are now working at, we use cd(change directory)  
```bash
$> cd path(argument to cd)
```


###Special Directories:

1. .(dot) 
	- represents the current directory
	```bash
	$> cd .(pwd does not change)
	```
2. ..(dot dot) 
	- refers to the parent directory of current directory  
	For example, pwd is now
	```bash
	/home/nanaeem/cs246/1151
	```
	now we enter
	```bash
	cd .. (pwd is now /home/nanaeem/cs246)
	```
	or
	```bash
	cd ../1155 (pwd is now /home/nanaeem/cs246/1155)
	```
	Note: dot dot can be used multiple times to refer to "grandparents"
	```bash
	cd ../../cs241 (pwd is now /home/nanaeem/cs241)
	```

3. ~(tilde) 
	- refers to the home directory
	```bash
	cd ~
	```
	equivalent to
	```bash
	cd 
	```

4. ~userid 
	- refers to userid's home directory
	```bash
	cd ~abcd
	```

###Listing Command

To list files:
```bash
$> ls (lists all files in the current pwd **except** for hidden files)
$> ls -a(lists all the files **including** hidden files)
```

####Wildcard Matching(Substitution)

To find all files that end with .txt(golbbing patterns)
```bash
$> ls *.txt
```
> Q: What happens when a globbing pattern is used?
>
> A: The shell notices the globbing pattern, performs the wildcard substitution, and replaces the glob with the results.

Note: single quotes(' ') and double quotes(" ")can **suppress the globbing pattern**.

###Cat
To display all the content of the file
```bash
$> cat filename
```
You can also simply enter
```bash
$> cat
```
and the program takes in keyboard input and echo it **immediately after you hit the enter**
```bash
$> cat
hello
hello
```
to end the program use ctrl + D (EOF) or ctrl + c(to kill it)

we can put the output in a new file using ">"
```bash
$> cat > outputfile.txt
```
However, ">" will **overwrite** the existing file, to append to an existing file we use
```bash
$> cat >> outputfile.txt
```
we can also input from a file
```bash
$> cat < sample.txt
```



