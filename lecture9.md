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
- `const int MAXIMUM = 100;`
- A constant **must be** initialized
- Declare as many things as possible(help catch errors)
- Prefer constants to magic numbers or # define maccros
- Can declare other things const
```C++
Node mynode = {5, NULL};
const Node cn = mynode;
```
but we __cannot__ do `n == mynode`  
>What does `int const *p = &n;` mean ?(`int n = 8;`)  
>It is a pointer to a constant int  
>We cannot change the value of n
>so `p = &x` is valid (p can be reassigned)  
>`*p = 5` is invalid (*p cannot be reassigned)  
  
- now consider `int *const p = &n;`
- constant pointer to (non-const) integer
	- `*p = 7;` can change *p
	- `p = &x;` cannot point to something else
- now `const int * const p = &n;`
	- constant pointer to a constant integer
	- cannot change where p points to
	- cannot change the value of what p points to
  

```C++
const long int * const a[5];
//array of 5 constatnt pointers to constant long integers
```

##Parameter Passing
```C++
void inc(int n) {
	n = n + 1;
}

int main() {
	int x = 5;
	inc(x);
	cout << x << endl;   //prints 5
}
```
- Parameters in C++ are passed by value
	- inc gets a copy of its parameter(x) and increments that copy
	- the original is unchanged
```C++
void inc(int *n) {
	*n = *n + 1;
}

int main() {
	int x = 5;
	inc(&x);
	cout << x << endl; //prints 6
}
```
- x's address is passed by value to inc
- inc modifies the data at that address and so changes are visible to caller
##`cin >> x;`
- Why do we say `cin >> x;`, and not `cin >> (&x);`
- Answer is that C++ provides another ptr-like type called a *reference*
```C++
int y = 10;
int &z = y; //z is a reference to y
```
- This is similar to a constant pointer
- similar to `int * const = &y;`
- Reference are like constant pointers with automatic dereferencing
- If we use `z = 12;` (not `*z = 12;`)and now y = 12
- `int *p = &z;`(z is an *alias* of y; so this gives the address of y)
- In all cases, z behaves exactly like y(z is another name for y)
  
###Things you **CANNOT** do with references
- Leave them uninitialized (e.g. `int &x;`)
- create a ptr to a reference(`int &*x = ...`)
- can create a reference to a ptr (`int *&p = ...`)
```C++
int main() {
	int n = 1;
	int m = 2;
	int *p = &n;
	int *&x = p;
	x = &m;
	cout << *p << endl; // prints 2
	
	*x = 3;
	cout << *P << endl; // prints 3	
```
- cannot create a reference to a reference(`int && r =...`)
- cannot create an array of references(`int &r[3] = {n, n, n}`)


