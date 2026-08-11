w/o oops, maintain karo dhyan se, repeat, no modularity, non real life programming, poor reusability, poor readability

w oop - bind prop and behaviour in a single unit supporting real world entities / objects


---


## copy constructor -

```cpp

// copy constructor -

Student( const Student& srcObj ){ // inside class
	this->name = srcObj.name; // yaha srcObj->name nahi ho sakta coz ptr nhi h
	this->rollno = srcObj.rollno; // uper wali line is very important for copy constructor
}

### 1. Standard Copy Constructor

A true copy constructor in C++ **must** take its parameter by reference—typically as a `const` reference (`const Student &srcobj`).

- **Why it's required:** If C++ allowed a copy constructor to take its argument by value (`Student srcobj`), invoking the copy constructor would require making a copy of `srcobj` first. Making that copy would invoke the copy constructor again, leading to an infinite recursion loop during compilation.
  
  


// call -
Student stu2 = stu1;   --> yaha stu1 as an argument jaega
 or
Student stu2( stu1 );  // dono same kaam karenge

```







## Deep vs shallow copy-

### 1. Shallow copy  (default copy constructor) -
- pointer variables point to the exact same memory location for both objects (as the original object).
- Two problems -
  1. Modifying the dynamically allocated memory through one object alters it for all copied objects.
  2. Potential double-free issues during destruction.

```cpp
#include <iostream>
using namespace std;

class abc
{
public:
    int x;
    int *y;

    // Parameterized Constructor
    abc(int _x, int _y) : x(_x), y(new int(_y)) {}

    // Default dumb Copy Constructor (Shallow Copy)
    /*
    abc(const abc &obj) {
        this->x = obj.x;
        this->y = obj.y; // Copies memory address directly (Shallow)
    }
    */
    
// Custom Copy Constructor (Deep Copy)
	abc(const abc &src) { 
		this->x = src.x;
		this->y = new int(*src.y); // Allocates separate heap memory and copies value
	}

    ~abc()
    {
        delete y; // Deallocates heap memory
    }
};

int main()
{ ... 

    return 0; // Note: May crash at runtime due to double deletion of same heap mmy due to shallow copy (~abc called twice for same `y` pointer)
}
```

### 2. Deep Copy (Custom Copy Constructor) -

In a **deep copy**, custom memory is explicitly allocated on the heap for any dynamically allocated variables so that the copied object gets its own unique copy of the underlying data.




----



## some things about constructor -


### 1. constructor call -
```cpp
Student ob1 = {"sd", 21, 18158};
```

### 2. default constructor call -
if no parameter constructor is made explicit or not -
```cpp
// 1. WITHOUT parentheses
Student* ob1 = new Student;
// 2. WITH parentheses
Student* ob2 = new Student();

// dono chalenge normally
```


### 3. constructor initialisation list -

```cpp
#include <iostream>
using namespace std;

class abc
{
    int x;
    int *y;
    const int z; // Const member variable must be initialized using initialization list

public:
    // Old style constructor
    /*
    abc(int _x, int _y, int _z = 0)
    {
        x = _x;
        y = new int(_y);
        z = _z; // ERROR: assignment of read-only member 'abc::z'
    }
    */

    // Constructor using Initialization List
    abc(int _x, int _y, int _z = 0) : x(_x), y(new int(_y)), z(_z) //here no error
    {
        cout << "in init list" << endl;
        // Additional setup logic can be written here if needed
    }
};
```


### 4. can constructor be made private ? -

- **Yes, constructors can be private.**
    
- **Why do it?**
    
    - To restrict direct instantiation from outside the class.
        
    - Essential pattern for **Singleton Design Pattern** (ensuring only one instance of a class exists).
        
    - Useful in **Factory Design Patterns** where creation logic is delegated to a separate manager/factory class.
        
- **How to instantiate?**
    
    1. Through a `friend class` or `friend function`.
        
    2. Through a `public static` member function inside the class itself.

```cpp
#include <iostream>
using namespace std;

class Box
{
    int width;

    // Private Constructor
    Box(int _w) : width(_w) {}

public:
    int getWidth() const
    {
        return width;
    }

    void setWidth(int _val)
    {
        width = _val;
    }

    // Declaring BoxFactory as a friend class so it can access the private constructor
    friend class BoxFactory;
};

class BoxFactory
{
    int count;

public:
    // Factory method to construct Box objects
    Box getABox(int _w)
    {
        return Box(_w); // Can call Box's private constructor because BoxFactory is a friend
    }
};

int main()
{
    // Box b(5); // ERROR: 'Box::Box(int)' is private within this context

    BoxFactory bFact;
    Box b = bFact.getABox(5);

    cout << b.getWidth() << endl; // Output: 5

    return 0;
}
```


### 5. can constructor be made virtual ? -
No

Reason -
1. **vptr is defined during ctor exe -**
   no vptr defined will lead to no Vtable that leads to no correct knowledge of function binding at runtime.
2. **Complete Information Needed:** Virtual calls tab use hoti hain jab hume exact type na pata ho (partial information). Lekin kisi object ko create karne ke liye compiler ko exact type pata hona mandatory hai (`new Derived()`). Isliye constructor kabhi virtual nahi ho sakta.



### 6. object creation of child class -

```cpp
class Parent {
public:
    Parent(int x) { /* ... */ }
};

class Child : public Parent {
public:
    // Explicitly calling the parameterized parent constructor first,
    // then initialisation list is follows
    Child(int _x, int _y) : Parent(x), x(_x), y(_y) { }
};
```


---

## Destructor -


### destructor call when -

```cpp
// if static obj making -
Student s1(); // destructor will auto called on program end

// if dynamic allocation -
Student *s2 = new Student();

delete s2; // manual destructor call karna padega
```


### can destructor be made virtual -
YES !

- in fact, it is highly recommended to always make parent class destructor as virtual.
- else, mmy leak can happen in child class, if UPPER CASTING is done, as only destructor of container (parent) class will be called due to early binding.
- ab perfect destructor chaining hogi (if upper casting kia h to and virtual bhi use karlia h)


---


## `this` keyword -
- `this` have reference of current object.
- regular instance methods and constructors have a hidden `this` pointer.
- the static member function does not receives `this` pointer.


---


## `static` keyword -

1. Any static member functions or data member can be called and used **without creating an instance** of the class using the scope resolution operator (`Class::function()` or `Class::x`).
   {`as they belong to the class itself (as a whole blueprint), not to any individual object instance.`}
2. a static data member very mandatorily needs to have a outside class definition while a static member function do not.

### 1. Static Data Members -
- all objects point to same data member ( that is declared static )
- or
- Static variables inside a class are shared across **all instances** of that class. Modifying it via one object updates it for all objects.

```cpp
#include <iostream>
using namespace std;

class abc
{
public:
    static int x, y; // Declaration of static data members

    void print() const
    {
        cout << x << " " << y << endl;
    }
};

// Definition / Initialization outside the class (Mandatory for static members)
int abc::x;
int abc::y;

int main()
{
    abc obj1;
    obj1.x = 1;
    obj1.y = 2;
    obj1.print(); // Output: 1 2

    abc obj2;
    obj2.x = 10;
    obj2.y = 20;

    // Changes made by obj2 reflect in obj1 because x and y are shared
    obj1.print(); // Output: 10 20
    obj2.print(); // Output: 10 20

    return 0;
}
```


### 2. Static Member Functions -
- a static member function cannot use non static data member that are related to an instance.
- the static member function does not receives `this` pointer.

```cpp
#include <iostream>
using namespace std;

class abc
{
public:
    int x, y;

    abc() : x(0), y(0) {}

    // Static member function
    static void print()
    {
        // Note: Cannot access non-static members (x, y) or 'this' pointer directly here
        printf("I am in Static %s\n", __FUNCTION__);
    }
};

int main()
{
    abc obj1;
    abc::print(); // Called directly using class scope

    abc obj2;
    abc::print();
    abc::print();

    return 0;
}
```



---



### mode of inheritance -
- child class m members kese ayenge with wht access specifier
- default mode of inheritance is private.

---

### struct vs class -
only 2 difference -
1. by default, members are private in class and public in struct.
2. by default, mode of inheritance is private in class and public in struct.




---

### number of objects -
- parent object is contained in the child object.
- in hierarchical inheritance also, each child object will be containing whole parent object data (individually)

---

## final -
only with - 
1. class (avoid further inheritance)
2. virtual member function (avoid overriding)

```cpp
virtual void speak() final { // now, no-one can override this method (from any child class)

}

class Base final { // now, no-one can inherit this class 

};
```


---

### Friend Class and Friend Function -

The `friend` keyword allows external classes or standalone functions to access `private` and `protected` members of a class.

```cpp
#include <iostream>
using namespace std;

class A
{
private:
    int x;

public:
    A(int _val) : x(_val) {}

    int getX() const { return x; }
    void setX(int _val) { x = _val; }

    // Declaring class B as a friend class of A
    friend class B;

    // Declaring standalone function print() as a friend function of A
    friend void print(const A &a);
};

class B
{
public:
    void print(const A &a)
    {
        // Directly accessing class A's private member 'x'
        // cout << a.getX() << endl; // Normal public method call
        cout << a.x << endl;        // Allowed because B is a friend class of A
    }
};

// Standalone Friend Function
void print(const A &a)
{
    // Directly accessing class A's private member 'x'
    cout << a.x << endl; // Allowed because print() is a friend function of A
}

int main()
{
    A a(5);
    
    // Testing Friend Class
    B b;
    b.print(a); // Output: 5

    // Testing Friend Function
    print(a);   // Output: 5

    return 0;
}
```

**Key Principles:**

- **Friendship is Granted, Not Taken:** Class `A` must explicitly declare `B` as its friend. Class `B` cannot force itself to be a friend of `A`.
    
- **Friendship is Not Mutual:** Declaring `B` as a friend of `A` does **not** make `A` a friend of `B`.
    
- **Friendship is Not Transitive:** If `A` is a friend of `B`, and `B` is a friend of `C`, `A` is **not** automatically a friend of `C`.
    
- **Friendship is Not Inherited:** Derived classes do not automatically inherit friendship permissions from parent classes.

