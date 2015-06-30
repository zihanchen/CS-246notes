#Lecture 17  

##Continued Encapsulation  

>What is the difference between the `class` and the `struct` in c++?  
>- Struct is public by default
>- Class is private by default  
  

>What does public mean?  
>- Anyone can access members  

  
>What does private mean?  
>- Accessible to class members and classes friends  <-------------------------------------|

```C++																		
class Vector {																 |
		int x, y;															 |
	public:																	 |
		Vector operator+(const Vector &v) const;						     |
};																			 |		
																			 |		
																			 |
 Vector Vector::operator+(const Vector &v) {								 |
	 Vector v1(x + v.x, y + v.y); //<---this is perfectly fine because of ---|
	 return v1;
}
```

##System Modelling  
Building an Object-Oriented system involves identifying the Key abstractions  
Drawing athe relationship can help aid in design, implementation and understanding  

###UML(Unified Modelling Language)  
Modelling a class  
   
| Vector |
| ------ |
| -x: integer |
| -y: integer |
| ...(methods) |
| ... |  
  
Visibility  
- `-` means private
- `+` means public
  
Show important parts that are needed for the design(not flag variables)  

When a class is instantiated  
1. Space allocated  
2. Default constructors/init list for all fields in declaration order  
3. Constructor body runs  
  
When an object is destoryed  
1. Destructor body runs  
2. Destructors invoked for all fields in reverse declaration order  
3. Space is deallocated  
  
Default constructor of class will call default constructor for each field  
if we don't have a default construtor we can:  
- Give a default constructor
- or using member initializing list

In vector example:  
```C++
class Plane {
		Vector v1, v2;
	public:
		Plane():v1(1,0,0), v2(0,1,0) {}
}
```
Embedding one object (e.g. vector) inside another (e.g. Plane) is called composition.  
Relationship between Plane and Vector is called an "owns - a" relationship  
A Plane object "owns-a" Vector object(infact, two of them)  
"owns - a"relationship typical characteristics:  
- If A owns B, then B typically has no identity outside of A(does not have an dndependent existance)  
- If A is destroyed then B is destroyed 
- If A is copied then B is copied (deep copy)  

Example: A car has four wheels - a wheel is part of a car  
- destroy the car implies destroying the wheels  
- copy the car implies copying the wheels(two cars don't share the same wheels)  
  
When modelling systems with classes, recognize the "owns-a" relationship and impement it with composition  
Composition in UML:  
```
-------			   ------------
|Plane|	    v1,v2  |Vector    |
|     |<>--------->|-x:integer|
|	  |			   |-y:integer|
-------			   ------------
```
`A<>------------>B` means A onws some # of B's
- 0..* = any # of B's 
- 2 = 2B's
- 1..5 = 1 to 5 B's
- can annotate with multiplicities , fields, anmes ,etc.  



##Aggregations
- Compare carcar parts in a car ("onws-a") vs car parts in a catalogue
- The catalogue contains the parts, but the parts have an independent existence  


