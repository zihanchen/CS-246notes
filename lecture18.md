#Lecture 19

##Destructor  
The three things that happen when an object is destoyed:  
1. Destructor body runs  
2. Destructors for fields run in the reverse declaration order  
3. Superclass(baseclass) destructor runs(this also has 3 steps)
4. Space is reclaimed  

>Always make the base class destructors virtual  

##Pure Virtual  
Say we have a Student base class and two subclass CoopStudent and RegularStudent  
both of them has fees() function  
```C++
class Student {
	protected:
		int numCourses;
	public:
		virtual int fees() = 0; //<--- this is a pure virtual method(which is a method has no implementation)
		//the student class is incomplete
		//Student s; <--- this is not going to work
		//since we cannot create objects of classes that have even one pure virtual method
		//Student is on ABSTRACT CLASS
}
```
Abstract classes:
- Can be used to organaize entities
- share common fields/methods
- polymorphism   
  
A derived calss inherits pure virtual methods from the base class,  
so the drived calss must implement ALL pure virtual methods to be considered "non-abstract" or concrete  
```C++
class RegularStudent: public Student {
	public:
		int fees() {
			return numCourses * 700;
		}
}
```


##Observor Pattern  
- Publish/subscribe system  
Subject: generates data; provides a subscribe method  

Observor: interested in data; provides a notify method  

##Decorator Pattern  
- Decorator is a component and decorator has a component(sometimes owns also make sense)  
```C++
Component *c = new Planewindow;
c = newScroll(c); //<---- this pointer is updated
c = newMenu(c);   //<---- this continues updating
```



