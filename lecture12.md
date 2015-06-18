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
- Only use `this` when you need to disambiguate a field/method from something else  
- Note methods can be overloaded in the same manner as other C++ functions

##Initializing Objects
```C++
Student Billy = {60, 70, 80};
```
this is okay but it is limited  
- can't ensure grades are between 0 and 100
  
What if we included a method whose only job is to perform object initialization  
- we call it a _constructor_
```C++
struct Student {
	int assigns, mt, final;
	Student(int assigns, int mt, int final) { //<--- this is a constructor
		this->assigns = assigns;
		this->mt = mt;
		this->final = final;
	}
};
