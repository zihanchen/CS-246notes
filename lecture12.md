#Lecture 12

##Intro to Classes  
By innovation of OOP(object-oriented programming)  
- can put functions inside of structures  
  
A class is essentially a struct that can contain functions  
- C++ has a keyword `class`
- An object is an instance of class
```C++
struct Student {
	int assigns, mt, final;
	float() {
		return assigns * 0.4 + mt * 0.2 + final * 0.4;
	}
};

  Student s = {60, 70, 80}
//   ^    ^
//   |    |
//   |    |
//class  object
```
- The function grad is called a _member function_(or _method_)
- assigns, mt and final... they are fields of the current object  
(the object upon which greade was called)
```C++
Student bruce = {...};
bruce.grade(); //method call, use bruce's assigns, mt and final
```
>How does this work?
>Formally, methods take a hidden extra parameter called `this`  

- `this` is a pointer to the object upon which the method was called  
(e.g`bruce.grade(); //then this == &bruce`)

