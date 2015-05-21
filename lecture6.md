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
		- gray-box testing
		- test harness 

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

##Testing Strategies  
- Unit Testing 
- Integration Test  
Once system is integrated:  
- Functional Testing
- Regression Testing
- System Testing
- Performance Testing
- Volume Testing 
- Stress Testing 
- Usability Testing: test whether users have the skill necessary to operate the system
- Security Testing: test whether programs and data are secure
- Acceptance Testing: does the system satisfies waht the client ordered  
  
    
##Tester  
- A program should **not** be tested by its writer, but in practice this often occurs.  
- Points to the need for a clear specification to protect both the client and developer.


##C++  
Let's look at a C program
```C
#include<stdio.h>

int main() {
	printf("Hello, world!\n");
	return 0;
}
```
Now see the C++ version:
```C++
#include<iostream>

unsing namespace std

int main() {
	cout<<"Hello, world!"<<endl;
	return 0;
}
```
- `#include<iostream> imports I\O descriptions
- output mechanism: std::cout << data << data << data ...\\
(where data can be numbers/srings etc.)
- std::endl prints a new line and forces a buffer finish
- All our C favourites are still available in C++(printf, stdio.h)
- main __must__ return int in C++
- using namsppace std allows us to refer to std::cout, std::endl as just cout and endl
- Return in main is optional. Value signals to shell successful(0) or unsuccessful(not 0) execution. No return statement results in 0 being returned  
  
###Compiling C++ programs
```bash
$> g++ myprog.cc
```
>a.out is default name for executable  
```bash
$> g++ myprog.cc -o myprog
```
>you can name you program using "-o"

