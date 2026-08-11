
design that separates interface from implementation.

eg - sort() method from # include <alogrithm is a simple interface provided to sort and it can be used for string, vector, etc multiple data types.


### abstract class -
class having at least one pure virtual function.

```cpp
class Student{
	public:
	virtual void eat() = 0;
};
```

- direct object creation of abstract class will make a compilation error

----

- abstraction is a design strategy
- it divides code into two categories - interface + implementation
- what it does is --->  any change in the implementation doesn't change anything for user (as interface is same)
- with any change in implementation, user just need to recompile at most
- 
- NOTE: interface class ka object kabhi nahi banta

```cpp
// Bird class is interface
class Bird {
public:
    virtual void eat() = 0;
    virtual void fly() = 0;
};


// classes inheriting Bird class are implementation
class sparrow : public Bird {
private:         // NOTE ---> is class m sab private h and cannot be directly used
    void eat() override {
        cout << "Sparrow is eating\n";
    }
    void fly() override {
        cout << "Sparrow is flying\n";
    }
};

class pegion : public Bird {
private:         // NOTE ---> same
    void eat() override {
        cout << "pegion is eating\n";
    }
    void fly() override {
        cout << "pegion is flying\n";
    }
};

-------

#include <iostream>
#include "bird.h"
using namespace std;

void birddoesSomething(Bird *&bird)
{
    bird->eat();
    bird->fly();
    bird->eat();
    bird->eat(); // no need for : sparrow->eat() specifically
    
 // mujhe different birds ke lie specifically call karne ki need nahi h
 // just call for bird
}

int main()
{ // NOTE --> m UPCASTING kar raha hu.
 // + polymorphism use kar raha hu
 // yahi abstraction hai   
    
    Bird *spro = new sparrow();
    birddoesSomething(bird);
    
    Bird *pgn = new pegion();
    birddoesSomething(bird);
    

 // mujhe different birds ke lie specifically create karne ki need nahi h
 // just create Bird container and done
}

```