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
Pint all words in global directionary that start with e and consist of 5 charactres.  
```bash
$> egrep "^e....$"
```
  
##Example 4  
  List all files in the current directory that do not contain cs246 in there name  
```bash
$> ls | egrep -v "cs246"
```
> -v invert the match  

