#Lecture 4  

##Last time
- "|"- or
- [...] - matches any single character  
  
##More egrep patterns  
- [n ...] - anything except  
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


