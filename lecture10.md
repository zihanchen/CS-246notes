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

Recall from C:  
```C
int size =  ;
int *p = malloc(size * sizeof(int));
...
free(p);
```
malloc/free are available in C++ but **DO NOT USE THEM**  
instead use new/delete
- Type aware, less error-prone(does work for you)

####Example
```C++
struct Node {
	int data;
	Node *next;
};

Node *np = new Node;
...
delete np;
```
now we try to allocating an array  
```C++
cin >> n;
int *arr = new int[n];
for (int i = 0; i < n; i++) {
	arr[i] = i * i;
}
delete []arr;
```
- array is on the stack
- new int[n] allocates on the heap
- array points to memory containing an array of n ints
- use delete to delete non-arrays
- use delete [] to delete arrays

#####Stack allocation vs Heap Allocation
- space for local vars(int x, y) allocated on stack
- local vars disappear when they go out of scope(stack is popped)
- the ptr np is on the stack, but Node itself is on the heap  
>Why use heap allocation?  
>You should always use stack allocation unless:
>- You don't know the size of the data in advance  
>- Need to access memory outside the scope in which it was allocated
>- large allocations may need  to be on the heap

###Example
```C++
Node getNode(){
	Node n ;
	return n;
}
```
- Expenseve as n has to be copied on return
```C++
node *getNode() {
	Node n;
	return &n;
}
```
- unsafe returns pointer to stack allocated data which is dead on return

```C++
Node *getNode() {
	Node *np = new Node;
	return np;
}
```
- OKay, returns pointer to still active heap-allocated data

##Operator Overloading  

```C++
struct Vec {
	int x;
	int y;
};

Vec add(const Vec &v1, const Vec &v2) {
	Vec v;
	v.x = v1.x + v2.x;
	v.y = v1.y + v2.y;
	return v;
}
```
but if we change the name of the function...  
```C++
struct Vec {
	int x;
	int y;
};

Vec operator+(const Vec &v1, const Vec &v2) {
	Vec v;
	v.x = v1.x + v2.x;
	v.y = v1.y + v2.y;
	return v;
}

int main() {
	Vec v1 = {1, 2};
	Vec v2 = {3, 4};

	Vec v6 = v1 + v2; //you can do this now
}
```
In fact, we can override most of the operators in C++  
We can give meanings to C++ operators for types we define.construct  
We can also overload `<<` and `>>`

```C++
struct Grade {
	int theGrade;
};

ostream &operator<<(ostream &out, const Grade &g) {
	out << g.theGrade << "%";
	return out;
}

istream &operator>>(istream &in, const 
```
Note that we return the in and out streams to facilitate cascades
- istreams will work with cin, ifstream and istringstreams
- similarly, for ostream and cout, ofstreams and ostringstreams
