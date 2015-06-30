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
| ------ |
| ... |
| ... |  
  
Visibility  
- `-` means private
- `+` means public
  
Show important parts that are needed for the design(not flag variables)
