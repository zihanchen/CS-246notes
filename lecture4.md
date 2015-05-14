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
