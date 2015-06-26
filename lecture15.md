#Lecture 15  

##Design Patterns
- Certain programming scenarios(problems) occurs frequently

####Singleton Design Pattern
- we have a class C and want to ensure it is only ever instantiated at most one  
regardless of how many times we attempt to create an instance

#######Static Members
- associated with the class itself, not a specific instance
	- static field
	- static method
  
```C++
struct Student {
	int assigns, mt ,final;
	static int numStudents;
	float grade() {
		return assigns * 0.4 + mt * 0.2 + final * 0.4;
	}
	Strudent(int assigns, int mt, int final): assigns(assigns), mt(mt) ,final(final){}
	static int printNumStudents() {
		cout << Student::numStudents << endl;
	}
};

Student::numStudents = 0;

int main() {
	Student::printNumStudents();// 0
	Student Billy(60, 70, 80);
	Student Bob(65, 75, 85);
	Student::printNumStudents();// 2
}
```
#####Static pointer to instance
- See code example in remote
- When should we deallocate a singleton?
- How do we know when all our clients are finished using it?  
A solution is to use reference counting in a destructor(once all clients have tried  
to delete, actually delete it)  
Another is just to delete it at the end of the main  
None of these sound particularly clean. They rely on good behaviour of clinents  
There is a C/C++ function called atexet form <cstdlib>  
atexit takes a pointer to a procedure that has no auguments and returns void and calls 
it at the end of the program execution  


>Note: atexit is a stack of thesefunctions(execution is last-in first-out)  
>- Also note that we are not giving a pointer of a destructor, since a dessturctor  
has an implicit this pointer

Problem: anyone can still create their own wallet-we don't force them to use our  
GetInstance method  

######Encapsulation  
Encapsulation: hide implementation to support abstruction(access control)  
Access control applies to types/classes and not objects
- all objects of a particular type/class have the same level of encapsulation
- Encapsulation is neither essential nor required to develop software  
  
However, not having it requires conventions and programmers are unreliable and don't  
always follow conventions  
It allows us to control the way our objects are used  
- want client to treat object as blackboxes
- Implementation details are hidden away
- can only interact via provided methods(the interface)
- this creates abstraction
- To keep implementation hidden(public vs private)
```C++
struct Vector {
	Vector(int x, int y): x(x), y(y) {} //public;
	private:
		int x, y;//private can't be accessed outside the scope of the struct
	public: 
		Vector operator+(const Vector &v1, const Vector &v2); //everyone can use
};
```
- Default visibility of a struct is public 
- Better to have default  visibility be private(less error prone)
- Switch frome struct to class(the default is now private)
```C++
class Vector {
	int x ,y;//private by default
	public:
		Vector(int x, int y): x(x), y(y) {}
		Vector operator+(const Vector &v1, const Vector &v2);
};
```
- The only difference between calss and struct is default visibility
- struct is public by default
- class is private by default
- further, we can use encaplsulation to preclude copying by making copy constructor  
and assignment operator private  
This is done to prevent coyping that may not make sense
- example :no need to copy our database object
- Again: keep fields private  
public fields imppy user can manipulate them in any way they want  
- can't maintain class invariants
- can't replace implementation without breaking client code  
If you want to provide field acess, write an accessor method  
```C++
class Vector {
		int x, y;
	public:
		int get x() const {return x;}
		int get y() const {return y;}
};
```
If you wan to let clients change fields, provide mutator method  
```C++
class Vector {
		int x, y;
	public:
		void setx(int new_x) {x = new_x;}
		void sety(int new_y) {y = new_y;}
};
```
Now suppose we don't want to previde accessors and mutators, but   
we do wan to preovide operator <<?  
- Issure: operator << needs to get x and y but we don't provide  
general access to anyone  
C++ provides a mechanism to allow __full__ access to trusted routines and classes called freindship  
```C++
Class Vector {
		int x, y;
	public:
		vector(int x, int y);
		...
	friend std::ostream &operator <<(std::ostream&out, const Vector &v);
};
```
now in .cc file we can  
```C++
ostream& opeartor<<(ostream& out, const Vector &v) {
	out << v.x << v.y;
	return out;
}
```
- friend functions cna see all of the of a class members but are not part of the class  
- Give your classes as few friends as possible
Much like real-life, friendship is not transitive.  
Your friend's friends are not necessarily your firends. You must  
state it explicitly
