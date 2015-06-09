#Lecture 11  

##The preprocessor

- The code you write is not the code that the compiler sees
- Before compilation the Preprocessor is run on your code  
- Preprocessor 

- Three main types of preprocessor statements
	- file inclusion
	- substitution
	- conditional inclusion

##File Inclusion
- File inclusion copies text from a file into a C/C++ program
- filename can be enclosed in <...> or "..."
- <...> means preprocessor only links in system include directories(e.g /usr/include)
- "..." links in current directory of file first, then system include directory
- C header files have a new convention
	- instead of `#include<stdio.h>` prefer `#include<cstdio>`

##Substitution  
`#define VAR VALUE`
- statement declares a preprocessor string variable and its value is all the text after var until end of line
- All instance of VAR  in the program are replaced with VALUE
- Prefer const variables instead (easier to debug)

##Conditional Inclusion
- Preprocessor has an if statement, which can be nested, to conditionally add or remove code from your program
- Conditional if uses some logical operators from C/C++
- but operands can only be integers or characters
```C++
#define Unix 1
#define Windows 2

#define OS Unix

#if OS == Unix
int main() {

#elif OS == Windows
int winMain() {

#endif


return 0;
}
```
>we can use this to comment out large block of code
```C++
#if 0
this will be commented out
#endif
```
we can also define variables in the command line
```C++
#include<iostream>

int main() {
	cout << X << endl;
	return 0;
}
```
this program has not defined X
```bash
>$ g++ -E -P -DX=42 define.cc
```
but we can run this  
it is equivalent to `#define X 42`  
We can also check if a preprocessor variable is defined or not
- `#ifdef VAR `returns true if VAR has been defined
- `#ifndef VAR` returns true if VAR has not been defined
>we can use this to debug our program
```C++
int main() {
	#ifdef DEBUG
		cout << "setting x = 1" << endl;
	#endif
	int x = 1;
	while ...
	...
}
```
>normally, the message will not be printed, but if you enter  
`$> g++ -DDEBUG debug.cc` the message will be printed  

##Separate Compilation
- Goal is to split code into composible modules which each provide:
	- interface: type definitions and function prototypes(.h files)
	- implementation: full definition for every provided function(.cc files)

- We can declare things many times, but only define them once  
>What if we want to put a variable in a .h file?  
>program will not link since every file that includes header will get its own copy  
of global variable  
>Solution:  
>In .h: `extern int globalNum;`  
>In one.cc: `int globalNum`  

Note: - `g++ -c` says to compile only, do not link files, do not build executable  
and output an object file(.o)
- object file is an "almost ready" executable just needs it's empty pieces to be filled in  
- main.cc and linAlg.cc include vectro.h and linAlg.h
- linAlg.h includes vector.h
- So we end up with two definitions of struct vec;
- Need to prevent files from being included more than once. How?
- Solution: Included guard
```C++
#ifndef __VECTOR_H__
#define __VECTOR_H__
```
