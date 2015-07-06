#Lecture 17

Last time we mentioned that Object-Oriented languages generally provide inheriance to made the book situation  
```C++
calss Book {
		string title, auther;
		int numPages;
	public:
		Book(...);
}; //Base class

class TextBook: public Book {
		string topic;
	public:
		TextBook(...);
}; //derived class (or subclass)

class ComicBook: public Book {
		string protag;
	public:
		ComicBook(...);
}; //derived class(or subclass)
```
- Derived calsses inherit fields and methods from the base class.
- So TextBook/Comic Book got title, author, nuPages from Book
- Any methods callable on Book can be called on TextBook/ComicBook
- whocan see member fields;
- title, author and numPages are private in Book -outsides cannot see them
  
>Can TextBook see them?(private fields)  
>No -even subclasses cannot see them  

>Public members, e.g getAuthor can be seen by everyone(outsides and subclasses)  


`Comic book cb;`  
- Can't access cb.author(private), but can call cb.getAuthor()(public)  
- How do we initialize ComicBook?(Need title, author, numPages, protag...  
```C++
class ComicBook: public Book {
		string protag;
	public:
		ComicBook(string title, string author, int numPages, string protag):
			title(title), author(author), numPages(numPages), protag(protag) {}
		//this won't work
};
```
Doesn't work for 2 reasons:  
1. title/author/numPages are not accessible in ComicBook  
	- When an object is constructed:
		1. Space is allocated  
		2. Superclass part is constructed  
		3. Field constructors are called  
		4. Constructor body runs  

	So our constructor should be:  
	```C++  
	ComicBook(string title, string author, int numPages, string protag):
		Book(title, author, numPages), protag(protag) {}
	```

2. Since Book has no default constructor the construct fails  

- To solve both problems, invoke Book's constructor in ComicBook's init list  
- If the super class has no default constructor, you MUST invoke a non-default constructor for the superclass explicitly in the subclass init list  

There are good reasons for keeping the superclass fields private from subclasses  
- But what if we really really want to give access to subclasses only
- C++ has **protected** visibility for that  

```C++
class Book {
	protected:
		string title, author;
		int numPages;
	//Accessible to Book and its subclasses, no one else
	public:
		Book(...);
};
```

Can now do:  
```C++
class TextBook: public Book {
		string topic;
	public:
		void addAuthor(string newAuthor) {
			author += newAuthor;
		}
};//ok
```

Not a good idea to give subclasses unrestricted access to fields  
- Better to make fields private and have protected accessors  
```C++
class Book {
		string title, author;
		int numPages;
	protected:
		string getTitle() const;
		void setAuthor (string newAuthor);
		//subclass can see these
	public:
		Book(...);
		bool isItHeavy();
};
```
We call the relationship between TextBook/ComicBook and Book the "is-a" relationship  
- a TextBook is a Book
- a ComicBook is a Book  
```
                 Book
				  ∆
				  |
			      |               Note:name represents a class model
		     -----------			 (i.e. they should in box with fields etc.)
			|           |
			|           |
		ComicBook    TextBook
```

We implement the "is-a" relationship using __public__ inheritance  

####When is a book heavy?  
- For an ordinary book: > 200 pages
- For a TextBook: > 400 pages
- For a ComicBook: > 30 pages  

Since inheritance defines an "is-a" relationship, we can do:  
- `Book b = cb; //cb is a comic book`

Is b heavy?
- which method runs, Book::isHeavy or ComicBook::isHeavy?
- No, b is not heavy Book::isHeavy runs  
- `Book b = ComicBook(...)`tries to fit a ComicBook object where there is only space for a Book object  
- What happens? The ComicBook is sliced   
- Protag field is chopped off  
ComicBood is roerced into a Book  
So Book b = ComicBook(...); converts the ComicBook into a Book and Book:isHeavy runs  
When accessing objects through pointers, slicing is unneccessary and doesn't happen  
But still, Book::isHeavy runs when we access pb->isItHeavy()  
- The same object behaves defferently depending on the type of the pointer it is accessed through  
- Compiler use the type of the pointer to decide which isItHeavy to run, Not actual type of underlying object  
How do we make a ComicBook act like a comicbook even when we use a book pointer  
- Declare method to be **virtual**  
```C++
virtual bool isItHeavy() const;
```
- ComicBook:isItHeavy runs in each case(pointers)
- virtual methods -choose which method to run based on actual type of(pointed to) object at runtime(Dynamic Binding)  

- Accomodates multiple types under one aubstrction __polymorphism__("many forms")  
- Note: This is why a function `void f(istream &in)` can return ifstream because ifstream is a subscalss of istream
