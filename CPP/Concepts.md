## local / global variable -

```cpp
int x = 2; // global

int main(){
	int x = 5;
	
	{
		cout << x; // gives: 5
		cout << ::x; // gives: 2
		// :: is used to access global variable anywhere		
	
	}
}

```

---

## mmy layout -

stack
 .
 .
 heap
 uninitialised data
 initialised data
 code.text


__IMPORTANT ->__
- stack data auto unwinds when program exe is done ( thus freeing stack mmy ).
- heap data should be manually deallocated by programmer.

---


## `const` keyword-

### 1. with variable -

1. n cpp-
- lvalue - value having a mmy location.
- rvalue - value does not having any mmy location.  ( like int literal 5 or reference variable / alias )

1. const variable ko read only variable banata h -- so access fast ho jata h

```cpp
const int x = 5;
x = 6; // error: not a valid modifiable lvalue


int const a = 8; // this is also valid
// vairable k naam se pehle kabhi bhi const keyword likh sakte h
```


### 2. with ptr -
```cpp
CONST DATA, NON-CONST PTR
int const *p = new int(5);
// or
const int *p = new int(5);



NON-CONST DATA, CONST PTR
int * const p = new int(6);



CONST DATA, CONST PTR
int const * const p = new int(7); 
```


### 3. with function -

```cpp
// fn. signature k baad
void speak() const {  // <-- like this

}
```


__IMPORTANT-NOTE ->__
- a const member function in a class cannot change values of any data member of class.  
- iska usage h - bhot tagda level ka
- if koi object const bana dia - to sirf vo methods call kar sakte hai, jo const h
```cpp
#include <iostream>
using namespace std;

class abc
{
    int x;
    int *y;
    int z;

public:
    // Constructor
    abc(int _x, int _y, int _z = 0)
    {
        x = _x;
        y = new int(_y);
        z = _z;
    }

    // Member functions marked as const
    int getX() const
    {
        return x;
    }

    void setX(int _val)
    {
        x = _val;
    }

    int getY() const
    {
        return *y;
    }

    void setY(int _val)
    {
        *y = _val;
    }

    int getZ() const
    {
        return z;
    }
};

// Function taking a CONST object reference
void printABC(const abc &a)
{
    // Calling getX(), getY(), and getZ() will give a compiler error 
    // unless getX(), getY(), and getZ() are declared as const member functions!
    
    // all this just coz we have taken `a` as const in parameter - compiler is so smart
    cout << a.getX() << " " << a.getY() << " " << a.getZ() << endl;
}

int main()
{
    abc a(1, 2, 3);
    printABC(a);
    return 0;
}
```

---

## Dynamic allocation -
```cpp
int* x = new int; // coz yaha mene koi initialisation nhi kari like `new int(6)` islie garbage value hogi
delete x;


int* arr = new int[50]; // for array
delete []arr;


// delete karne se pointer jaha point kar raha tha vaha se hat jaega
// and randomly point karega
cout << *x << endl;
```


---


## nullptr vs NULL -
- NULL can implicitly convert to integer ( while function overloading )
- nullptr overcomes this `NULL's` limitation and never converts to integer ( converts to pointer only )


---


## macros -
text copy paste during pre processing 
```cpp
 #define PI 3.14 
 #define MAXX(a,b) (a>b ? a : b)
```


---


## inline fn -
replace code at compile time unlike macros that do at pre processing (before compiling)
```cpp
inline void say(){
	cout <<"hi";
}
```


---


## default parameters -
```cpp
int add(int a, int b = 5){
	return a+b;
}

//NOTE: right to left order is important to assign a default valu
```


---


## Exception Handling -

```cpp
#include <iostream>
#include <exception>

try {
    // Your code here
}
catch (const std::exception& e) {
    // Catches standard exceptions and reads the message
    std::cout << "Standard exception: " << e.what() << std::endl;
}
catch (...) {
    // Catches anything else (like raw ints or custom types)
    std::cout << "Unknown non-standard exception caught." << std::endl;
}

```