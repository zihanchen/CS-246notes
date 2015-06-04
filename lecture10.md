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

