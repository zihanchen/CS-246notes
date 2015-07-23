#Lecture 24  

Last time: Dynamic casting  

##Exception  

dynamic casting with reference  
```C++  
TextBook t(...);
Book &b = t;
TextBook &t1 = dynammic_cast<TextBook &>(b);
```
if b is a reference to a textbook, then t1 is a reference to that textbook  
However, reference cannot be NULL!!  
- A bad-cast error(exception) occurs if b is not a reference to a textbook  
  
Other examples:  
- when new fails: bad-alloc  
- when the index used for vector is out of range
  
By default, C++ programs terminate if an exception thrown/raised  
We can use try catch block to catch the exception and recover the exception after the catch block  
(i.e code after catch will still be executed **if that catch handle the right exception**)  
- When an exception occurs, the call stack is repeatedly popped util an appropriate handler(catch block) is found  
- This is "stack unwinding"  
- Error Recovery can be a multi-step process
```C++  
try {
	...
	...
	try { ... }
	catch (someException s) {
		partly recovery;
		throw someotherException(---); //<--- option 1: throw some other exception that will be dealt by higher catch
		throw s;                       //<--- option 2: throw the exact s again
		throw;						   //<--- option 3: rethrow waht as caught
	}
}
catch {...}
```
ADVICE:  
1. catch by reference to prevent slicing and copy  
2. All C++ library exceptions ingerit from a base "exception" class   
3. In C++ you can throw anything (int)  
  
Catch all exceptions:  
```C++  
try {
	//somecode
}  
catch(...) {
	//somecode
}
```
the "..." really mean explicitly the three dots  

Recall the problem last time  
```C++  
Book *p = TextBook(---);
Book *q = TextBook(---);
*p = *q;
```
We have one solution that is make the assignment operator virtual and implement it  
```C++  
TextBook::operator=(const Book &others) {
	TextBook &tother = dynamic_cast<TextBook &>(other);
	Book::operator=(other);
	topic = tother.topic;
	return *this;
}
```  

##Exceptions are a game changer  
```C++  
void f() {
	MyClass *p = new MyClass;
	MyClass q;
	...
	...
	delete p;
}
```
However, this code can still leak memory, if there is a function g() in f() that throws an exception `delete p` p is never executed   
We want to write code that is exception safe   
C++ guarantee:  
- The destructors for stack allocated objects are always called(even during stack unwinding due to exceptions)  


An exception safe code:  
```C++  
void f() {
	MyClass *p = new Myclass;
	MyClass q;
	try {
		g();
	}
	catch(...) {
		delete p;
		throw;
	}
	delete p;
}
```
ADVICE:  
- good idea to use stack allocation when you can
- never let destructor throw an exception  


##RAII(Resource Acquisition Is Initialization)  
every resource should be wraped in a stack allocated object.(whose job is to reclaim the resource)  

C++ provides a template class:  
```C++  
class auto-ptr <T>
```
