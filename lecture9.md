#Lecture 9

Recall:  
- Overloaded functions: same name, different parameter types or number of parameters  
- Default parameters: use default values if given for unspecified parameters

##Pointers and Arrays  

#####Example  
```C++
#include <iostream>
using std::cout;
using std::endl;
int main() {
	int i = 10;

	int *ptr;

	ptr = &i;
	*ptr = 2;

	int a[4] = {1, 2, 3, 4};

	ptr = a;

	cout << a[i] << endl; //prints 3 ; *((a)+(i))
	cout << ptr[i] << endl; //also prints 3

	cout << 5["abcdef"] << endl; // prints f
	cout << 2[ptr] << endl; // prints 3
}
```

##Bit field 
```C++
struct S {
	int i : 3;   //3 bits
	int j : 7;   // 7 bits
	int k : 6;   // 6 bits
}s;
```
we can limit the numbers to the specified bits  

##Constants  
- const provides a mechanism to ensure a variable's value cannot change
- `const in MAXIMUM = 100;`
