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
