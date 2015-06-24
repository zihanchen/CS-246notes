#Lecture 14  

##Continued constructor
- Be careful with constructors that take one parameter
- Single argument constructor create implicit conversions
```C++
struct Node {
	int data;
	Node *next;
	Node(int data, Node *next): data(data), next(next) {}
};

void f(Node N) {
	cout << "here" << endl;
}


int main() {
	Node myNode = 4;
	Node mynode2(5, &myNode);
	//this can form a linked list
	int x = 4;
	f(4); // this is also fine;
	return 0;
}
```
- Accidentally pass on `int` to a function execting a `Node` 
- It is silently converted, compiler doesn't signal an error  
- Potential errors are not enough
- Good idea: Disable implicit conversions by making constructors *explicit*
```C++
explicit Node(int data, Node *next):...{}
```
- now it gives us error  

##Destructors

- When an object is destroyed(stack allocated goes out of scope, heap allocated is deleted)  
a special method called a destructor runs.
- A destructor is a special method is a special method used to perform unitialization at object deallocation  
- An object can have at most one destructor
- Classes have a default destructor that doesn't do much: call destructor for member field
- The name of the destructor is the object name, refixed with `~`  
- We only define our own destructor if an object is not contiguous(e.g. composed of multiple pieces, files, dynamically allocated memory, etc)  
- A contiguous objec like student does not need a destructor
- Nodes are not contiguous , so it needs a destructor
```C++
struct Node {
	...
	...
	~Node() {
		delete next;
	}
};
```
What happens when an object is destroyed?  
- destructor is called first and then memory is freed
- delete next recursively calls `*(n.next)`'s destructor
- Therefore, whole list is reclaimed
- Now: delete np; frees the whole list

##Const is back
- int f(const Node &n) {...}
- const object arise often, especially in parameter lists
- What is a const object. Its fields cannot be medified  

What about calling methods on a const object?
- Problem method may modity fields and so violate const
- We can call methods that promise not to modify fields
```C++
struct Student {
	int assigns, mt, final;
	float computeGrade() const {
		return assigns * 0.4 + mt * 0.2 + final * 0.4;
		}
};

int main() {
	const Student s = {60, 70, 80};
	cout << s.computeGrade << endl;
	return 0;
}
```
Compiler checks that const methods do not modify fields. Only const methods can be called on const objects  
- But maybe we want to collect usage stats on Student objects
```C++
struct Student {
	int assigns, mt, final;
	mutable int numMethodCalls; // make a field mutable
	float computeGrade() const {
		numMethodCalls++;
		return assigns * 0.4 + mt * 0.2 + final * 0.4;
		}
};

int main() {
	const Student s = {60, 70, 80};
	cout << s.computeGrade << endl;
	return 0;
}
```
- We can't call grade on const students  
- We want to update numMethodCalls even if object is const: declare field `mutable`  
- mutable fields can be canged even if object is const

##Assignment Operator
```C++
Student Billy(60, 70, 80);
Student bob = billy; // copy constructor
Student s; //default constructor
s = billy; //copy but no construction
```
- Assignment opeartor uses compiler supplied version	
```C++
Node &Node::operator=(const Node &other) {
	if (this == &other) return *this;//this is for self assignment
	Node *tmp = next;
	next = other.next ? new Node(*other.next) : 0;
	data = other.data;
	delete tmp;
	return *this;
}
```
Why is this dangerous?
- n = n;  
- deletes n and then tries to copy n to n ---undefined behaviour  
- ALWAYS ---when writing operator=, check for self assignment  
  
Alternate copy and swap 
```C++
void Node::swap(Node &other) {
	int tmpdata = data;
	data = other.data;
	other.data = tmpdata;

	Node *tmpnext = next;
	next = other.next;
	other.next = tmpnext;
}

Node  &Node::operator=(Node other) {
	swap(other);
	return *this;
}
```

##Rule of Three  
If you need to write a custom version of:  
- Copy Constructor
- Assignment operator
- Destructor

Then you likely need to write a custom version of all three  
Notice: operator`=`is a member function, not a stand alone function  
When an operator is declared as a member function, `this`plays the role of the LHS argument  
- We cannot move a function as a member function if the first argument is not the struct type
- So it must be external  
What about I/O operations?
- means we have to do `v << cout` which is strange  
So do fine operator `<<` as external  
Certain operators must be members:  
- operator`=`
- operator`[]`
- operator `->`
- operator `()`
- operator `T()` //cast operator
