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
		- white-box testing 
		- bray-box testing 

###Example: Calculates income tax  
income < 10k : no tax
10k <= income < 100k : 10%  
income >= 100k : 20%  
  
----------------------------------------------------  
Equivalent Partition
1. 5000
2. 75000  
3. 200000

