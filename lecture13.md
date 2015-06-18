#Lecture 13
  
Heap allocation Student(`Student *billy = new Student(60, 70, 80)`  
Advantages of constructors(since they are just member functions)  
- default parameters
- overload etc.

```C++
struct Student {
	Student(int assigns = 0, int mt = 0, final = 0) {
		this->assigns = assigns;
		this->mt = mt;
		this->final = final;
	}
};

int main() {
	Student steve; //0,0,0
	Student tony(90,100) //90,100,0
}
```
- Every class comes with a default constructor(no arguments), which calls  
the default constructor on any members that have them
- But, the built-in constructor goes away as soon as you provide a constructor
```C++
struct Vector {
	int x,y;
	Vector(int x, int y) {
		this->x = x;
		this->y = y;
	}
};

int main() {
	Vector v2(1, 2); // valid
	Vector v; //Error (the original constructor was gone)
}
```
We also lose C-style structure initialization when we define a constructor  
```C++
Vector v = {1, 2, 3}; // this is invalid if you defined a construtor
Vector varr[10]; //this is also invalid when you defined a constructor
Vector *vp = new Vector[10]; //invalid
```
- Arrays of objects require a default constructor when declared as above
- If you have a default constructor, then reassign elements as necessary afterwards  
>What if a struct contains constants or references?  
>Initialize them
```C++
struct MyStruct {
	int const myConst = 5;
	int z;
	int &myRef = z;
}

int main() {
	...
}
```
Each instance of MyStruct shall be able to get its own myConst and myRef  
Why should they be the same  
>Can we initialize them in the constructor?
>No, it's too late. Need to be initialized by then.  
>Need to perform initialization before constructor body runs.  
>What happens when an object is created?  
>1. Spare for the object is allocated  
>2. Default constructors called for field members  
>3. Our initialization need toe go here  
>4. Constrcutor body runs.  

Solution: Member initialization list  
here is an example:  

```C++
struct MyStruct {
	const int myConst;
	const int &myRef;
	MyStruct(int c, int &r): myConst(c), myRef(r){}
};
int main() {
		int z = 5;
		MyStruct m(10, 2);
	
}
```
  
An initialization list can be more efficient then setting the fields in the body, Why?  

```C++
struct A {
	A() { cout << "A ctor" << endl; }
	A(int x) { cout << "A ctor x" << x << endl; }
};

struct B {
	A a;
	A c;
//	B() {this->a = A(5); }
	B() : c(1), a(5) {}
};
int main () {
//	A a;
	cout << "Constructing B now" << endl;
	B b;
}
```
- Since the default constructor runs first, then we reassign n in the body(assigning twice)  
Initialization of fileds happens  
**in the order in which they are declared**  
regardless of the order of initialization  
Consider
```C++
Student bruce(60, 70, 80);
Student oswald = bruce;
```
How does this initialization occur?  
The copy constructor is called for constructing one object as a copy of another  
Every class comes with a default constructor(call default constructor on he fielsd.  
Recall we lose this if we define our own constructor  
A copyt construct  
- an assignment operator
- destructor


##Copy Constructor
```C++
struct Student {
	Student(int assigns, int mt, int final): assigns(assigns), mt(mt), final(final) {
		cout << "Default ctor is being called: << endl;
	} //<--- this is a constructor
	Student(const Student &other) : assigns(other.assigns),
									mt(other.mt)
									fianl(other.final) {
		cout << "Copy ector is being called" << endl;
									}// <--- this is a copy constructor
};

int main() {
	Student s(60, 70, 80);
	Student s2 = s; //<-- s2 is the same as s, and it will call the copy constructor
	return 0;
}
```
- Constructor with a const reference parameter of calss type is used for initialization, called a copy constructor  

>When is the default copy constructor not correct?  
>simple copy of fileds, only first node is copied  
>we call this a shallow copy
```C++
struct Node {
	int data;
	Node *next;
	Node (int data, Node *next): data(data), next(next) {}
	Node(const Node &n): data(n.data), next(n.next == NULL ? NULL : new Node(*nnext)) {}
};
```
- above is a deep copy( copy the whole list)
										

