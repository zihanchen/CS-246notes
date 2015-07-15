#Lecture 21  


##C++ Template 
We have a linked list class  
```C++
class Node {
	int data;
	Node *next;
};
```
but this list can only store integer, what if we want to store string? or chars?  
Of course, we can create another class, but that is a lot duplication.  
So, we use templates:  
Template: parameterize a class on one or more type variables  
- Replace the `int` type in class Node with a type variable 
 
```C++
template < typename T > class Node {
		T data;
		Node < T > *next;
	public:
		Node(T data, Node <T> *next): data(data), next(next) {}
		T getData const {return data;}
		Node < T > *getNode() const {
			return next;
		}
};
```
Now we want to use this template  
```C++
Node <int> *t = new Node<int>(1, new Node<int>(2, new Node<int>(3, NULL))); //<--- this creates a linked list of int
Node <char> *c = new Node<int>('a', new Node<char>('b', new Node <char>('c', NULL))); //<--- this creates a linked list of char
Node < Node <int> > *l = new Node< Node <int> >(t, NULL); //<--- this creates a linked list of linked list of int
```

##Standard Template Library(STL)  
- Vector  
- Map  

####Vector  
Vector: dynamic length arrays
- Vector will internally resize as needed  
- Parameterized on one type  
```C++
#include<vector>

int main() {
	vector <int> vec;
	vec.push_back(22); //<--- put an int in the end of the array
	vec.push_back(12);
	for(int i = 0; i < vec.size(); i ++) {
		cout << vec[i] << endl; //<--- the range is unchecked(the compiler does not check for whether the index is valid)
		cout << vec.at(i) << endl; //<-- this is range checked 
	}
	vec.pop_back(); //<-- remove the ;last element
}
```
We know that there is a cool way to iterate through an array, that is using pointer
```C++
for (int *p = v; p < size; p ++) {
	cout << *p << endl;
}
```
Now we got a even cooler way, the __iterators__  
back to the vector case:
```C++
for ( vector<int>::iterator i = vec.begin(); i != vec.end(); i ++ ) {
	cout << *i << endl;
}
```
we can also have a reverse iterator  
```C++
for ( vector<int>::reverse-iterator rit = vec.rbegin(); rit != vec.rend(); rit ++ ) {
	cout << *rit << endl;
}
```
we can also erase the element in the vector:  
```C++
vec.erase(vec.begin());   //<--- remove the first element
vec.erase(vec.rbegin());  //<--- remove the last element 
vec.erase(vec.end() - 1); //<--- this is doing the same thing as one above
```

####Map  
A map allows any type for the key and value  
```C++
#include<map>

int main() {
	map< string, int> m;
	m["abc"] = 1;
	m["def"] = 2;
	cout << m["def"] << endl;
	if(m.count("abc") //<--- this returns true if "abc" is found and false otherwise
	for(map<string, int>::iterator mit = ...) {
		(*mit).first; //key
		(*mit).second; //value
	}
}
```
Map iteration goes through the map in sorted key order

####Visitor Design Pattern  

Double Dispatch: Choose a method to run based on a run time type of two objects  
