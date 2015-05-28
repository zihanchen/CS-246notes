#Lecture 8

##Example: I\O manipulator  
```C++	
#include<iomanip>

int main() {
	int i = 95;
	cout << hex << i << endl; //print in hex
	cout << i << endl; //this also print in hex, this is "sticky"
	float price = 2.00;
	cout << fixed << showpoint << setprecision(2) << price << endl; //show all the 
}
```

print numbers frome 1 to 20 in 3 diferrent ways:
```C++
#include<iostream>
#include<iomanip>

int main() {
	for (int i = 0; i < 20 ; i ++) {
		cout << dec << setw(3) << i < oct << setw(3) << i << hex << setw(3) << i << endl;
		}
}
```

##File I/O


```C
#include<stdio.h>

int main() {
	char buf[255];
	FILE *file = fopen("suite.txt", "r");
	while(1) {
		fscanf(file, "%s", buf);
		if (feof(file)) break;
		printf("%s\n", buf);
	}
	fclose(file);
}
```
 
```C++
#include<iostream>
#include<string>

using namespace std;

int main() {
	ifstream file("suite.txt");
	string s;
	while (file >> s) {
		cout << s << endl;
	}
}
```
- Typically, C-style I/O is going to be faster due to less abstractions but often not noticeable  
- Anything you can do with cin, you can do with ifstream
- Anything you can do wich cout, you can do with if stream

###String Streams   
- C++ provides us with string streams 
`#inlcude<sstream>`
- `istringstream`:for reading from a string
- `ostringstream`:for writing to a string

```C++	
#includ<sstream>
using namespace std;

int main() {
	string s;
	while(cin >> s){
		istringstream ss(s);
		int n;
		if (ss >> n) cout << n << endl;
		}
}
```

###C++ Strings  
- Recall ,C strings are character arrays(`char *`, `char[]`)
	- must be terminated by `\0`
	- Need to explicitly manage memory
	- easy to overrite `\0`
	- does not store pertinent information with string(e.g. length)
- C++ solves this by providing a string type(#include<string>)
	- C++ strings grow and shrink as needed(manage their own memeory)
	- Safer and stores pertinent info, like length

###String operations
Say we have string s1, s2
- Equality: s1 == s2
- Inequality: s1 != s2
- Comparison: s1 <= s2( lexicographic comparison )
- Extract individual characters(s[1], s[2]...; s1[0] == ' ')
- Concatenation string: s3 = s1 + s3(s3 += s1)

###Default function parameters
- can have a default value for parameters
- can call a function without all parameters if parameters have a defaut value
```C++
void printSuitefile(string name = "suite.txt") {
	ifstream file(name.c_str());
	string s;
	while (file >> s) cout << s << endl;
}
```
- Default parameters must be ata the end of the parameter list

###Overloading

In C:
```C 
int negint(int i) {
	return -i;
}

int negbool(bool b) {
	return !b;
}
```
In C++: 
```C++
int neg(int n) { return -n; }
bool neg(bool b) { return !b; }

int main() {
	cout << neg(3) << " " << boolalpha << neg(true) << endl;
}
```
- We call this overloading
- The compiler(g++) will use the # and types of parameters to pick the right function("neg" to call)
- Overloads **MUST** differ in either # or type of some parameters
- cannot overload on return type

