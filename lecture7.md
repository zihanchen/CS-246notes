#Lecture 7  

##C++ I/O  
- There are two kinds of input/output
- Formatted I/O: transfer data with implicit conversion of internal 
values to from human readable form
- Unformatted I/O: transfer data without conversion, e.g. internal representation
of integers and floating points(binary numbers)  

##Standard I/O Streams
- C++ privids 3 (actually 4) input and output stream objects

(inlcuded via #include<iostream)  

- source screen: cout << "Hello World" << endl
- cin: reads from standard input
- cout: prints to standard output (buffered)
- cerr: prints to standard error (unbuffered)

##C++ I/O operators  
- << : "put to" (output)
- >> : "get from" (input)
- cout << x : print x to stdout
- cerr << x : print x to stderr
- cin >> x : gets x from stdin  
>arrow points in direction of information flow

##Example  
```C++
#include<iostream>

using std::cout;
using std::cin;
using std::endl;

int main() {
	int x, y;
	cin >> x >> y;
	cout << x + y << endl;
	return 0;
}
```
cin by default will ignore any whitespace  
conseder`cin >> x >> y;`  
Looks for the next two integers on stdin ignoring any whitespaces  
between them
There could be any number(>= 1)of spaces, tabs and newlines between x and y
>What if next value is not an integer?  
>- statement fails: variable is not assigned (return its previous value)  
>What if input exhausted(eod)?  
>- same  

- if read fialed: cin.fail() returns true
- if eof: cin.fail() and cin.eof() both return true
- won't happen until we attempt to read and fail  

```C++
#include<iostream>

using namespace std;

int main() {
	int i;
	while (true) {
		cin >> i;
		 if (cin.fail()) break;
		 cout << i << endl;
		 }
}
```
- There is and implicit conversion between cin and void*
	- if(cin):
		- true if !cin.fail() (return non-Null value)
		- false if cin.fail() (null returned for cin)  

###About >>
- `>>` is the C right bit shift operator:  
a >> b shift a bits to the right by b spots
- but when cin is on 'the left' side of >>, then it 
is the "get from" operator  
- operator >>
	- function which can be called in a special way
	- Input: cin(istream), data(various types)
	- Output: return cin (istream)
	- That's why we can do the following
	```C++
	cin >> x >> y >> z; //returns cin
	```
so we can improve the previous program into:
```C++
int main() {
	int i;
	while (c >> i) {
	cout << i << endl;
	}
}
```
>Why is this not the ideal way to do this?  
>cannot recover in cawe of invalid input  

```C++
int main() {
	int i;
	while (true) {
		if (!(cin >> i)) {
			if(cin.eof()) break;
			else {
				cin.clear();
				cin.ignore();
			}
		else {
		cout << i << endl;
		}
	}
}
```

##Reading Strings  
- C++ provides the type std::string(via `#include<string>`) for 
working with strings
- Basically, it is a better version of C-string(char *)
```C++
#include<string>
#include<iostream>
using namespace std;

int main() {
	string s;
	cin >> s;
	cout << s << endl;
}
```
- Semantics reads the next characters into a string
(Skipping leading whitespaces) and stops one a  
- Will read from current position to next new line into Semantic



