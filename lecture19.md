#Lecture 19


##Observer Pattern  
1. If only one subject class, can merge subject and concrete subject classes  
2. If state is trivial(e.g. just need to be notified that somthing happened), then getState doesn't need to be used  
3. If the subject is also the observer (e.g. cells in a grid) then you can merge these classes too  


##Decorator Pattern  
- Suppose we want to add functionality to something dynamically, but still maintain the original object(e.g power ups in video game)  
- Want to enhance object at runtime -add functionality and features  
- Examples:
	- Windowing System
	- Start with a basic window
	- add scroll bar
	- add menu
- we want to choose the environments at runtime
- Class component -defines the interface operations your object will provide  
- Concrete component -implememnts the interface  
- Decorators all inherit frome Decorator which inherits from component
- Thus every Decorator is-a Component AND every Decorator has-a a Component
- Eg. Window with a scrollbar is a kind of window that has a pointer to the underlying plane window  
- Eg. Window with a scrollbar and a menu is a window, has a pointer to a window with a scrollbar which has a pointer to a plain window  
- All would inherit from Abstract Window so window methods can be used polymorphismally on all of them
- Decorator pattern is similar Template patter  
- Except instead of defining a relationship between super and subclasses, we are defining relationships between subclasses(based upon superclass)
