#Lecture 7  

##C++ I/O  
- There are two kinds of input/output
- Formatted IO: transfer data with implicit conversion of internal 
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

using std::out 

int main() {
	int x, y;
	cin >> x >> y;
	cout << x + y << endl;
	return 0;
}
```

