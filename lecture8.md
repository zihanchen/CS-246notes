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

##Declaration before use
- In C++, we must declare something before we can use it
- So, how is mutual recusion done?
```C++
bool odd (unsigned int n); //A forward delaration

bool even(unsigned int n) {
	if (n == 0) return true;
	else return sood(n - 1);
}

bool odd(unsigned int n) {
	if (n == 0) return true;
	else return even(n - 1);
}
```
- Solution use a foward declaration  

There is an important distinction between  
- declaration: only asserts the exstance of an entity
- definition: full definition, including allocaiont of space, if needed

##Pointers

Recall
```C++
int n = 5;
int *p = &n;
cout << p << endl  //hex # address
cout << *p << endl //5
```
```C++
int **pp;
pp = &p;
**p = 6;
```

##Arrays
```C++
int a[] = {1, 2, 4, 8};
```
- The name of an array is just short hand for the address of the first element of the array &a[0]
- `*a` is equivalent to `a[0]`
- `*(a+1)` is `a[1]`
- arrays do not have index bounds checks(we can do a[1000])

##Structure  
Structs are a mechanism to group related data
- hetrogenious types
```C++
struct Node {
	int data;
	Node *next;
};
```

