#Lecture 23 


See an example:  
```C++
TextBook b1("CS246", "Nomair", 200, "C++");
TextBook b2("CS136", "Dave", 100, "C");
Book *pb1 = &b1;
Book *pb2 = &b2;
*pb1 = *pb2;
```
- object assignment through pointers  
- print b1 after the assignment prints CS136, Dave, 100, **C++**  
- The assignemnt is perform a partial assignment since the Book assignment operator is called
- so we have to make it virtual  
```C++
virtual Book&Book::operator(const Book&) {...}

TextBook&TextBook::operator=(const Book& b) {
	//How do I access the right hand side topic?
}
```  
So we do not want this happen  
Let's make books' assignment operator protected  
- This will work, but it prevent actual Book objects to be assgined  
- Advise: make base classes abstract, and implement a protected operator=


##Casting  
- C style cast tend to get lost in the code  
- C style cast is too powerful  

####Static_cast  
for casts that just make "sense"   
```C++  
int m = 9;
int n = 2;
std::cout << m / n << std::endl; //<--- this prints "4"  
std::cout << static_cast< double >(m) / n << std::endl; //<---- this prints "4.5" 
```  
```C++  
Book *pb = ...; //we know that pb is pointing to a textbook  
TextBook *t = static_cast<TextBook *>(pb);
```
- an unchecked cast 
- trust me I know what I am doing  
- Behaviour is undefined if cast is incorrect  
- Static_cast can only be used if there is IS A relationship virtual -downcast  

####Reinterpret_cast  
This has no restrictions  
```C++ 
Vec v;
Student *s = reinterpret_cast<Student *> (&v);
```
- Behaviour is completly compiler depended  
- relies on objects are represented in memory  

####Const_cast  
- add/remove `const`  
```C++  
void libraryfunc(int *g) {} //the function does not promise not to change g  
void foo(const int *p) {
	libraryfunc(p); // <--- you cannot do this  
	libraryfunc(const_cast<int *> (p)); //<--- you can do this  
}
```
- The behaviour is undefined if the libraryfunc changed g  

####Dynamic_cast  
```C++  
vector<Book *> collection;
for(---) {
	TextBook *t = dynamic_cast <TextBook *>(collection[i]); // this tentatively check whether this is a TextBook pointer or not  
	if(t) std::cout << t->getTopic() << std::endl;
}
```
- if the cast suceeds(i.e. collection[i] is a TextBook then t point to it  
- otherwise t is set to NULL
- dynamic_cast only works if the class hierarchy has at least one virtual method  


##RTTI(Run Time Type Infomation)  
```C++
string shatIsIt(Book *b) {
	if(dynamic_cast <TextBook *>(b)) {
		cout << "TextBook" << endl;
	}
	else if(dynamic_cast <Coimc *>(b) {
		cout << "Comic" << endl;
	}
	else cout << "Book" << endl;
}
```
We should use virtual 


