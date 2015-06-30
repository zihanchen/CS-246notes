#Lecture 17  

##Continued Encapsulation  

>What is the difference between the `class` and the `struct` in c++?  
>- Struct is public by default
>- Class is private by default  
  

>What does public mean?  
>- Anyone can access members  

  
>What does private mean?  
>- Accessible to class members and classes friends  <------------------------|

```C++																		
class Vector {																 |
		int x, y;															 |
	public:																	 |
		Vector operator+(const Vector &v) const;						     |
};																			 |		
																			 |		
																			 |
 Vector Vector::operator+(const Vector &v) {								 |
	 Vector v1(x + v.x, y + v.y); <---this is perfectly fine because of -----|
	 return v1;
}
```
