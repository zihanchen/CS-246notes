#Lecture 22  

Last time: Visitor Design Pattern  

#Continued Visitor Design Pattern  
We have two tpyes of enemy: Turtle, Bullet  
We have two tpyes of weapon: Stick, Rock  
Want the dffect of __strike__ to depend on both, the type of Enemy + type of weapon  
This is a DOUBLE DISPATCH  
```C++
Enemy *e = ...
Weapon *w = ...
e->strike ( *w);  //<--- this does not depend on w, only on e
```
now get to the enemy class and weapon class:  
```C++
class Enemy {
	public:
		virtual void strike (Weapon &w) = 0;
};

class Turtle: public Enemy {
	public:
		void strike(Weapon &w) {
			w.useOn(*this);  //this performs the second dispatch
		}
};

class Bullet:public Enemy {
	public:
		void strike(Weapon &w) {
			w.useOn(*this); 
		}
};

class Weapon {
	public:
		virtual void useOn(Turtle *t) = 0; //this can
		virtual void useOn(Bullet *b) = 0;
};

class Stick: public Weapon {
	public:
		useOn(Turtle &t); //using stick on turtle
		useOn(Bullet &b); //using stick on bullet
};

class Rock: public Weapon {
	public:
		useOn(Turtle &t); //using a rock on turtle 
		useOn(Bullet &b); //using a rock on bullet
};


Enemy *e = ...
Weapon *w = ...
e->strike( *w);
```


Back to the book example:  
We want a catalogue that:   
- tracks Books by author
- TextBooks by topic
- Comic by protag  

to do this we could have a "catalogue" field in Book and an update method in Book  
```C++  
class Book {
		string title;
		string author;
		int numPages;
		map<string, int> catalogue;
	public:
		virtual update(catalogue);
};
```
- Adding the catalogue code to all classes, clutters these classes  
- what if source code is not available  

We can use the VDP to add new features to a class hierarchy without:  
- needing source code
- clutterthe class hierarchy(separation of concerns)  

AS LONG AS the class hierarchy accepts visitors  
```C++ 
class Book {
	public:
		virtual void accept(BookVisitor &b) {
			b.visit( *this);
		}
};

class TextBook:public Book {
	public:
		virtual void accept(BookVisitor &b) {
			b.visit( *this);
		}
};

class ComicBook: public Book {
	public:
		virtual void accept(BookVisitor &b) {
			b.visit( *this);
		}
};

class BookVisiter {
	public:
		virtual visit(Book &b) = 0;
		virtual void visit(TextBook &tb) = 0;
		virtual void visit(ComicBook &cb) = 0;
};
```


##Dependency(using include and forward declaration)  
in a.h:  
```C++
class A {...};
```
in b.h:  
```C++
#include "a.h"
class B: public A {...};
```
in c.h:  
```C++
#include "a.h"
class C { A myA;};
```
Both cases needs to know what is inside A thus using include

d.h:  
```C++
class A;
class D {
	A *myAp; //size of the pointer is fixed so the include is not needed
	void foo();
};
```
in d.cc:  
```C++  
#include "a.h"
void D::foo() {
	myAp->bob();
}
```
in e.h:  
```C++  
 class A;
class E {
	A foo(A x);  //complier only need to know there exists an A in header, and include that in the .cc implementation
};
```

##Copy Constructor and Assignment Operator in Inheritance  


```C++  

TextBook::TextBook(__,__,__,__):Book(__,__,__), topic(topic) {}

TextBook c = b; //<-- calls the one you get for free  

TextBook(const TextBook &other):Book(other), topic(other.topic) {}  //free one (default)  

TextBook &TextBook::operator=(const TextBook &other) {
	Book::operator=(other);
	topic = other.topic;
	return *this;
}
```


