#Lecture 4  

##Last time
- "|"- or
- [...] - matches any single character  
  
##More egrep patterns  
- [^ ...] - anything except  
- Accept an optional space
```bash
$> egrep "[Cc][Ss] ?246" index.shtml
```

- ? means 0 or 1 of the preceding expression
- * means 0 or more of the preceding expression
```bash
$> egrep "(cs) *246" index.shtml
```

- . matches any single character  
(so .* matches any sequence of chars just like * in globbing)  
```bash
$> egrep "cs.*246" index.shtml #<-- matches lines that contain a string starting with CS  
and ending with 246
```

- ^ matches beginning of line 
```bash
$> egrep "^cs246" index.shtml
```

- $ matches the end of line
```bash
$> egrep "^cs246$" index.shtml #<-- line that just contain "cs246"
```

- + matches 1 or more occurrences of the preceding pattern  
```bash
$> egrep "^.+$" index.shtml #<-- all non-empty lines
```
>Note: can use {x, y} to show occurences between x and y
```bash
$> egrep "[aeiou].*[aeiou] {2,}" index.shtml  #2 or more occurences
```
- \ supresses the special meaning characters  
so `\.` just a dot character
  
##Example 1  
Print all lines with even length
```bash
$> egrep "^(..)*$" index.shtml
```

##Example 2  
Print all files in the current directory whose name contains exactly one "a".  
```bash
$> ls | egrep "^[^a]*a{^a}*$"
```

##Example 3  
Print all words in global directionary that start with e and consist of 5 charactres.  
```bash
$> egrep "^e....$"
```
  
##Example 4  
  List all files in the current directory that do not contain cs246 in there name  
```bash
$> ls | egrep -v "cs246"
```
> -v invert the match  

####Precedence: Repetition > concatination > alternation  
- put expressions in **parenthesis** to **override** the precedence  
  
##Permissions  
- `$> ls -l` gives a long "long form" directory listing

```bash
$> -rw-r----- 1 present staff 25 13 May 22:36 abc.txt
```
- groups:  
	- a user can belong to one or more groups
	- a file can be associated wth a single group  
- type:
	- - means ordinary file
	- d means a directory  
- permissions: 3 groups of 3 bits
	- first 3 is user bits then  group and then other bits
		- user bits: what the files owner can do with the file
		- group bits: what members of the file's group(other than owner) can do
		with the file
		- other bits: what all other can do with the file
	- if it is on then there is a letter, otherwise there is a dash  

####What these files mean depends on the type of the file

|Bit	|Ordinary File	|Directory	|
|-------|:-------------:| ----------|
|r		|contents can be read|directory's contents can be read|
|w		|contents can be modified|directory can be modified|
|x		|can be executed as a program|directory can be open|

>Note: if a directory's execute bit is not set, you cannot enter that directory nor can you
>access any subdirectory within that directory

####Changing a file's permissions chmod  
```bash
$> chmod mode file
```

|Ownership Class	|Operator	|Permissions|
|-------------------|:---------:|----------:|
|u(user)			|+ (add)	|r			|
|g(group)			|- (remove)	|w			|
|o(other)			|=(set exactyl)|x		|
|a(all)				|			|			|


##Variables  
Sometimes we want to save data and reuse data in the shell  
We can use shell variables for this:
```bash
$> x=1 #no space here!
$> echo $x
$> 1
```
> To fetch a value of a variable, precede with $  
>When setting a variable do not use $  
>Note: All variables have type stirng, X is the sting "1"  

####Several "Global" variables set up by us:  
Most important for us is `${PATH}`
- it is a list of directions 
- when you type a command the shell will searches these directories \\
in order for the program with that name

>we cannot run the program in the current directory because the current directory is not 
>in the PATH. However, we can add it to the PATH

```bash
$> ./a.out #you can now run the program a.out
```
- should not contian ".", especially as the first element

