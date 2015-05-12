#lecture 3

##Pipes

Other than imput and output redirection this is another way to do this 

###Pipes( | )

Allow us to use the output of one program as the input to another(sets second program's STDIN to the first program's STDOUT)

>Unix Philosophy:
>"Write programs that do one thing and do it well"
>Then you can compose these programs together to do <strong>amazing</strong> things.

####Example 1

How many words are there in the first 20 lines of the file foo.txt?

```bash
>$ head -20 foo.txt | wc -w
>$ 165
```

####Example 2

Suppose files s1.txt, s2.txt, s3.txt...,etc. contain lists of words,

one per line print a duplicate-free list of all words that occur in any of s*.txt

```bash
$> uniq  #remove repeated lines(need to be sorted)
```

```bash
$> sort #sort the file
```

so the answer is 
```bash
$> cat s*.txt | sort | uniq
```

####Example 3

What are the top 10 retweets in file cs246.out file format
tweet id | # of retweets | original author | tweet ?

So we want to sort by the # of retweets

```bash
$> sort -r -n --key=2,2 -t '|' cs246.out | sort -u -s --key=4,4 -t '|'| sort -r -n --key=2,2 -t '|' | head -10
```

####Example 4

Who are the top 10 people with a most retweeted tweet in cs246.out?

```bash
$> sort -r -n --key=2,2 -t '|' cs246.out | sort -u -s --key=3,3 -t '|'| sort -r -n --key=2,2 -t '|' | head -10
```

####Exercise
Who are the top 10 most active (post most number of tweets of retweets)?  



What if we want the out put of a program as the <strong>argument</strong> of another? Is this possible?

>Put the command in backquotes

```bash
$> echo "Today is `date` and I am `whoami`"
$> Today is Tue 12 May 2015 12:15:04 EDT
```

>and _single quotes suppress this_

```bash
$> echo 'Today is `date` and I am `whoami`'
$> Today is `date` and I am `whoami`
```

There is another way, which is putting it in the "$"

```bash
$> echo Today is $(date)
$> Today is Tue 12 May 2015 12:15:04 EDT
```
>But "$" is better to use

```bash
$> ls `echo `ls``  #system does not understand this
```

```bash
$> ls $(echo $(ls))  #this one is fine
```

>What is the difference between pipes and input/output redirection?
>
>Pipes are used between commands.It sends the output of one command to
>the input of another command input and output redirection is between
> a command and a file.


###Find 
	- find is a command to search for file in a directory hierarchy
	- $> find [path] [expr]
	- start at path and list files matching expr
	- if path is omitted, start at current dircetory "."
```bash
$> find . -name "*.txt"
```

####Pattern matching in tex Files 
	- fool grep
	- egrep 
	- usage: egreap pattern file(s)

#####Example 1

Print every line in index.shtml that contains cs246

```bash
$> egrep cs246 index.shtml
```

>What kinds of patterns can we search for?
>
>Regular expressions(**NOT THE SAME AS GOLBBING PATTERNS**)


#####Example 2  

Search for cs246 or CS246

```bash
$> egrep "CS246|css246" index.shtml
```
or 
```bash
$> egrep "(CS|cs)246" index.shtml
```

There is another quotes
```bash
$> egrep "[Cc][sS]246" index.shtml
``` 
is equivalent to
```bash
$> egrep "(C|c)(S|s)246" index.shtml
```

>[] matches any one of the characters beween [ and ]
>
>[abc] is equivalent to (a|b|c)


