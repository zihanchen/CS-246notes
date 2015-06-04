#Lecture 10

>So, why does `cin >> x;`work?  
>`istream &operator >> (istream &in,int &n);`  
>Because it takes x as a reference parameter  


- Pass-by-value(e.g `int f(int n) {...}`): copies the argument
- Therefore, if the argument is big, the copy is expensive  
e.g  
```C++
struct ReallyBig {
	int arr[1000000];
};

int f(ReallyBig rb) {...} // copies the whole structure

int f(ReallyBig &rb) {...} //pass an alias:efficient but allows changes to propagate to caller  

int h(const ReallyBig &rb) {...} //efficient: no copy and parameter cannot be changed
```
- Advice: Prefer passy-by-reference-to-const over pass-by-value for anything larger than an int  
- `int f(int &n){...} // calling f(5) is invalid`
- cannot initialize a reference with a literal value. If n changes ,cannot change literal
- `int g(const int &n){...} //now f(5) is valid`
- since n can never change compiler will allow thiis  

##Dynamic Memory Allocation
---
Recall from C:  
```C
int size =  ;
int *p = malloc(size * sizeof(int));
...
free(p);
```
