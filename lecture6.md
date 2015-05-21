#Lecture 6  

Say we have a script:  
```bash
$> cat src 
pwd
cd ..
pwd
```
and we execute it 
```bash
$> bash src
/users/cs246/1155
/users/cs246
```
but the **actual**pwd is still in 1155, because we are running this  
script in a sub-shell. If you want to have an effect on the actual  
shell we can use
```bash
$> source src
```
and now our pwd is in cs246  

##Testing  
- Hunman Testing  
	- code inspection
		- eata errors
		- logic errors
		- interface errors
	- walkthrough
	- desk checking
- Machine Testing
	- test case design
		- black-box testing
			- equivalent partitioning
			- boundary value testing
			- error guessing
			- extreme test cases
			- black-box case can and *should be* written **before**  
			development as it can reveal problems with requirements  
			or understanding
		- white-box testing 
			- test every decision alternative at least once
			- test all the functions and modules
			-
		- bray-box testing 

###Example: Calculates income tax  
income < 10k : no tax
10k <= income < 100k : 10%  
income >= 100k : 20%  
  
----------------------------------------------------  
#####Equivalent Partition  
1. 5000
2. 75000  
3. 200000
  
#####Boundry cases  
1. 999999
2. 10000  
3. 10000.01  

#####Edge cases  
1. 0
2. 800000000000000

#####Error Guessing  
1. 5000
2. "dog"
