
# C# Crash Course (for someone who knows C++)

Mindset: C# ka syntax C++ + Java ka mix h. Sabse bada mental shift -> **sab kuch class ke andar rehta h** (no free functions), aur memory manual nahi, GC (garbage collector) handle karta h.

---

## 1. Program structure

```csharp
using System;

namespace MyApp
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World");
        }
    }
}
```

- `using` = C++ ka `#include` + `using namespace` combined.
- `Main` hamesha class ke andar, static hona mandatory (jaise ek static entry point).
- No header files. No `.h`/`.cpp` split. Ek `.cs` file me sab.
- (C# 9+ me "top-level statements" bhi chalte h, direct `Console.WriteLine("Hello");` bina Main likhe — interview me shayad na pooche but agar dikhe code me to confuse mat hona)

---

## 2. Data types
In C#, _every single type_ ultimate derives from `System.Object`

```csharp
int x = 5;
double d = 5.5;
float f = 5.5f;      // f suffix mandatory
bool b = true;        // not "bool true/false" issue - same as cpp (0/1 nhi)
char c = 'a';
string s = "hello";   // capital S, string is a CLASS (reference type), not char array
// System.String = string (same in csharp)
decimal money = 10.5m; // high precision, used for currency - C# specific, no cpp equivalent
var y = 10;            // type inference, compiler decides at compile time (not like JS var)
```

- `string` is immutable (like Java) — har modification naya object banata h.
- `var` != C++ `auto` in behavior conceptually — but same idea: type set at compile time, can't change type later.

---

## 3. ⭐ Value types vs Reference types — BIGGEST C# SPECIFIC CONCEPT

Yeh cpp me directly nahi hota (cpp me tum khud decide karte ho stack/heap via `new`). C# me **type khud decide karta hai**.

||Value Type|Reference Type|
|---|---|---|
|Keyword|`struct`, `int`, `bool`, `enum`, etc|`class`, `string`, `array`, `object`|
|Stored|stack (usually)|heap|
|Copy behavior|full copy on assignment|reference copy (points to same object)|

```csharp
struct Point { public int x, y; }   // VALUE type
class PointC { public int x, y; }   // REFERENCE type

//FULL DEEP COPY
Point p1 = new Point();
p1.x = 5;
Point p2 = p1;      // FULL COPY
p2.x = 10;
// p1.x is still 5

//SUPER SHALLOW COPY
//**no new object is created in the heap at all**.
PointC c1 = new PointC();
c1.x = 5;
PointC c2 = c1;      // REFERENCE COPY (same as cpp pointer)
c2.x = 10;
// c1.x is now ALSO 10 (same object)
```

**Interview favorite question:** "struct vs class in C#?" -> value vs reference type, struct can't have destructor/inheritance (except interfaces), struct better for small lightweight data.

---

## 4. Arrays & Collections

```csharp
int[] arr = new int[5];
int[] arr2 = { 1, 2, 3, 4, 5 };
int[] arr3 = new int[] { 1, 2, 3 };

arr.Length          // NOT arr.length, not sizeof(arr)/sizeof(arr[0]) like cpp

// Dynamic-size collections (like cpp vector / STL)
List<int> list = new List<int>();
list.Add(10);
list.Remove(10);
list.Count          // NOT list.size()

Dictionary<string, int> dict = new Dictionary<string, int>();
dict["key"] = 5;    // like cpp map, but hashmap (unordered) underneath
dict.ContainsKey("key");
```

Common STL -> C# mapping:

- `vector<T>` -> `List<T>`
- `map<K,V>` -> `Dictionary<K,V>` (unordered), `SortedDictionary<K,V>` (ordered like cpp map)
- `set<T>` -> `HashSet<T>`
- `pair<A,B>` -> `Tuple<A,B>` or `(A,B)` (value tuples, C# 7+)
- `stack<T>` / `queue<T>` -> `Stack<T>` / `Queue<T>`

---

## 5. Properties — C# specific, no direct cpp equivalent

Instead of writing `getX()`/`setX()` manually everywhere, C# has **properties**:

```csharp
class Student
{
    private string name;

    // full property
    public string Name
    {
        get { return name; }
        set { name = value; }   // "value" is implicit keyword = param passed
    }

    // auto-implemented property (compiler generates hidden backing field)
    public int RollNo { get; set; }

    // read-only property
    public int Age { get; private set; }
}

// usage - looks like accessing a field directly, but get/set run under the hood
Student s = new Student();
s.Name = "abc";        // calls set
Console.WriteLine(s.Name);  // calls get
```

**Interview favorite:** "What's the difference between a field and a property?" -> field is raw data member, property is a field wrapped with get/set accessors (encapsulation without needing explicit getX/setX method calls).

---

## 6. Classes, Constructors, Destructors

```csharp
class Student
{
    public string name;
    public int rollNo;
    
    
    //constructors can be made private
  //  - **Factory Methods**: Forces developers to instantiate the class through //specialized static methods rather than direct constructors.

//- **Utility / Static Classes**:


    // constructor - same idea as cpp
    public Student(string n, int r)
    {
        name = n;
        rollNo = r;
    }

    // NO copy constructor concept in C# by default!
    // Reference types copy by reference automatically (see section 3)
    // You'd write a manual Clone()/copy method if deep copy needed

    // destructor / finalizer - RARELY used, GC handles cleanup automatically
    ~Student()
    {
        // cleanup code - called by GC at some undetermined time, NOT deterministic like cpp
    }
}
```

**KEY DIFFERENCE from your cpp notes:**

- No `delete` in C#. GC automatically frees unused heap objects. You don't manually manage memory.
- Destructor (`~ClassName`) exists but its timing is **non-deterministic** (GC decides when). Don't rely on it for critical cleanup (like closing files).
- For deterministic cleanup (files, DB connections, etc) -> implement `IDisposable` + `Dispose()` method, use with `using` statement:

```csharp
using (var file = new StreamReader("a.txt"))
{
    // file automatically Dispose()'d at end of block, deterministic
}
```

---

## 7. Access Modifiers

```csharp
public       // accessible everywhere
private      // only within same class (DEFAULT for class members, same as cpp class default)
protected    // class + derived classes
internal     // accessible within same assembly/project only (NEW - no cpp equivalent)
protected internal   // protected OR internal
private protected    // protected AND internal (C# 7.2+)
```

- Default access for class members = `private` (same as cpp `class`).
- `internal` is the C# equivalent of "package-private" — no direct cpp analog.

---

## 8. Inheritance & Polymorphism

```csharp
class Animal
{
    public virtual void Speak()   // "virtual" needed, same concept as cpp
    {
        Console.WriteLine("Animal speaks");
    }
}

class Dog : Animal    // ":" instead of cpp's public/private inheritance syntax
{
    public override void Speak()   // "override" keyword MANDATORY in C# (not optional like cpp)
    {
        Console.WriteLine("Dog barks");
    }
}
```

**Big differences from cpp:**

1. Only **single class inheritance** allowed (`class Dog : Animal` — can't inherit 2 classes). Multiple inheritance achieved via **interfaces** only.
2. `override` keyword is **mandatory** when overriding — cpp me optional tha (`override` cpp11+ optional safety check, yaha zaroori h).
3. To hide a base method without polymorphism -> use `new` keyword instead of `override`.
4. `sealed` = cpp's `final`:

```csharp
sealed class Cannot_Be_Inherited { }
public sealed override void Speak() { }  // cannot be overridden further
```

5. `base` keyword = cpp's explicit parent constructor call:

```csharp
class Dog : Animal
{
    public Dog() : base() { }   // like Parent(x) in cpp init list
}
```

---

## 9. Abstract classes vs Interfaces

```csharp
abstract class Shape
{
    public abstract double Area();     // no body, must override - like cpp pure virtual (=0)
    public void Print() { Console.WriteLine("Shape"); }  // normal method allowed
}

interface IShape        // convention: prefix "I"
{
    double Area();       // no body, always "pure virtual" implicitly
    // C# 8+ allows default implementations in interfaces too, but keep it simple for interview
}

class Circle : Shape, IShape    // can inherit 1 class + multiple interfaces
{
    public override double Area() { return 3.14 * r * r; }
}
```

**Interview favorite Q: abstract class vs interface?**

- Abstract class: can have some implemented + some abstract methods, fields, constructors. Single inheritance only.
- Interface: (traditionally) no implementation, no fields, no constructors. A class can implement MULTIPLE interfaces — this is how C# achieves "multiple inheritance."

---

## 10. Static keyword — same concept as cpp

```csharp
class Counter
{
    public static int count = 0;   // shared across all objects, same as cpp static member

    public static void Increment()  // no "this", callable without object
    {
        count++;
    }
}

Counter.Increment();   // Class.Method(), NOT ClassName::Method() like cpp
```

- `static class` (whole class static, e.g. `Math`) — can't be instantiated, only static members allowed. No cpp direct equivalent (closest = namespace of free functions).

---

## 11. Exception Handling

```csharp
try
{
    int x = 5 / 0;
}
catch (DivideByZeroException e)
{
    Console.WriteLine(e.Message);
}
catch (Exception e)   // generic catch-all, like catch(...) in cpp
{
    Console.WriteLine("Something went wrong");
}
finally
{
    Console.WriteLine("Always runs");   // cleanup code, guaranteed execution
}

// custom exception
class MyException : Exception
{
    public MyException(string msg) : base(msg) { }
}

throw new MyException("custom error");
```

---

## 12. Boxing / Unboxing — very common interview Q, no cpp equivalent

```csharp
int x = 10;
object obj = x;        // BOXING: value type -> reference type (heap allocation happens)
int y = (int)obj;      // UNBOXING: reference type -> value type (back to stack)
```

- Performance cost hota h boxing/unboxing me (heap alloc + type check). Interviewers love asking "why is boxing expensive?"


### 1. **Why it was used (The "Universal Slot"):**
Boxing allows a value type (`int`, `float`, `struct`) to fit into any method or collection designed to hold an `object` reference (e.g., legacy `ArrayList` or `Console.WriteLine(object obj)`). It acts as a bridge so a single reference parameter can accept _literally anything_.

SIMPLY -
ek parameter set kara bas
and multiple types of data accept kar sakte h


### 2. **Why it's not recommended as a pattern:**
Relying on `object` parameters forces C# to give up compile-time type safety and causes heavy performance penalties (heap allocation + Garbage Collection overhead).

### 3. **How C# Solved This (Generics):**
In modern C#, you rarely need to box value types manually to pass them around. C# 2.0 introduced **Generics** (`List<T>`, `void MyMethod<T>(T item)`). Generics allow you to pass any data type efficiently **without boxing**, giving you both type safety and performance.


**Bottom Line:**
Boxing is a built-in fallback mechanism so value types can fit into reference-type containers (`object`), but passing arguments as `object` is avoided in modern C# in favor of Generics (`<T>`).

---


## 14. Generics — same idea as cpp templates

```csharp
class Box<T>
{
    private T item;
    public void Set(T val) { item = val; }
    public T Get() { return item; }
}

Box<int> b = new Box<int>();
b.Set(5);

// generic method
T Max<T>(T a, T b) where T : IComparable<T>
{
    return a.CompareTo(b) > 0 ? a : b;
}
```


---


## 13. Nullable types & null handling

```csharp
int? x = null;              // int can't normally be null, "?" makes it nullable
int y = x ?? 5;              // null-coalescing: if x is null, y = 5

string s = null;
int len = s?.Length ?? 0;    // null-conditional "?." - avoids NullReferenceException
```


---

## 15. Delegates, Lambdas, Events — commonly asked, no direct cpp equivalent (closest = function pointers/std::function)

```csharp
// delegate = type-safe function pointer
delegate int MathOp(int a, int b);

MathOp add = (a, b) => a + b;    // lambda expression
Console.WriteLine(add(2, 3));    // 5

// events - built on delegates, used for pub-sub / callback patterns
class Button
{
    public event Action OnClick;   // Action = built-in delegate type, no params no return
    public void Click() { OnClick?.Invoke(); }
}
```









### Delegates & Events — Quick Revision Notes

### 1. Delegates
It can point to both **static** and **instance** functions.

- **Definition:** A type-safe function pointer or variable that holds a reference to a method with a matching signature (return type and parameters).
    
- **When to use:** Used when you need to pass a method as a parameter to another method.
    
```csharp
// 1. Declare delegate matching method signature
public delegate void Calculator(int x, int y);

// Methods matching the signature
public static void Add(int a, int b) => Console.WriteLine(a + b);
public static void Multiply(int a, int b) => Console.WriteLine(a * b);

// 2. Instantiate and invoke
Calculator calc = new Calculator(Add);
calc(20, 30); // Output: 50
```

---

### 2. Multicast Delegates

- **Definition:** A delegate that holds references to multiple methods with the same signature, executing them sequentially in a single invocation.
    
- **Mechanism:** Methods are chained using the `+=` operator.
    
```csharp
Calculator calc = Add;
calc += Multiply; // Chaining another method

calc(20, 30); 
// Output: 
// 50  (from Add)
// 600 (from Multiply)
```

---

### 3. Anonymous Delegates

- **Definition:** Delegates pointing directly to inline methods defined without an explicit name (anonymous methods).

```csharp
// Inline method body without declaring a named function
Calculator calc = delegate(int a, int b) 
{
    Console.WriteLine(a + b);
};

calc(10, 20); // Output: 30
```

---

### 4. Events vs. Delegates

- **Definition:** An event is a notification mechanism that acts as an encapsulation and security wrapper around a delegate.
    
- **Key Differences:**
    
    - **Dependency:** An event depends on a delegate and cannot exist without one.
        
    - **Security & Encapsulation:** Delegates allow direct external invocation and reassignment. Events restrict external code to subscribing (`+=`) or unsubscribing (`-=`), preventing external callers from resetting or directly invoking the underlying delegate chain.



---

## 16. LINQ — Language Integrated Query (C# specific, big selling point, likely to be asked)

Lets you query collections SQL-style:

```csharp
List<int> nums = new List<int> { 1, 2, 3, 4, 5, 6 };

var evens = nums.Where(n => n % 2 == 0).ToList();      // filter
var doubled = nums.Select(n => n * 2).ToList();         // map
int sum = nums.Sum();
int max = nums.Max();
var sorted = nums.OrderBy(n => n).ToList();
```

- `Where` = filter, `Select` = map/transform. These two alone answer most LINQ interview questions.

---

## 17. `==` vs `.Equals()` vs `ReferenceEquals()`

`==` is kind of polymorphed.
- for value based comparison ----> it acts like `a.Equals(b);`
- for reference based ----> acts like `ReferenceEquals(ob1,ob2);`

```csharp
string a = "hi";
string b = "hi";
a == b;              // true (value comparison for strings, overridden)
a.Equals(b);          // true

object o1 = new object();
object o2 = new object();
o1 == o2;             // false (reference comparison by default for objects)
ReferenceEquals(o1, o2);  // false, explicitly checks if same memory reference
```

---

## 18. Quick C++ -> C# translation table

|C++|C#|
|---|---|
|`#include`|`using`|
|`cout <<`|`Console.WriteLine()`|
|`cin >>`|`Console.ReadLine()`|
|`->` for pointer access|not needed, `.` works for everything (no explicit pointers for objects)|
|`NULL` / `nullptr`|`null`|
|`delete`|not needed (GC), or `Dispose()` for unmanaged resources|
|`virtual` + optional `override`|`virtual` + **mandatory** `override`|
|`final`|`sealed`|
|multiple inheritance|multiple **interfaces** only|
|`struct` = class with public default|`struct` = VALUE type (fundamentally different from `class`)|
|templates|generics (`<T>`)|
|`const`|`const` (compile-time) / `readonly` (runtime-assignable-once, in ctor)|
|namespace|`namespace` (same)|
|function pointer|`delegate`|
|`arr.size()`/`sizeof` trick|`arr.Length` (array), `list.Count` (List)|
|header + cpp split|single `.cs` file|
|manual copy constructor|not a thing; ref types share, value types auto-copy|

---

## 19. Rapid-fire interview answers (memorize these lines)

- **Is C# fully OOP?** Mostly yes (unlike cpp) — but has value types (struct, int, etc) which aren't objects in the classical sense, though they can still call methods via implicit boxing.
- **Managed vs unmanaged code:** C# runs on CLR (Common Language Runtime) — "managed" means CLR handles memory/GC. cpp compiles to native "unmanaged" code.
- **Why no multiple inheritance for classes?** Avoids the Diamond Problem — C# solves it by allowing multiple interface implementation instead.
- **What is boxing?** Converting value type to reference type (heap alloc) implicitly.
- **String vs StringBuilder:** string is immutable (every modification = new object, expensive in loops). Use `StringBuilder` for heavy string manipulation in loops.
- **ref vs out params:**
    
    ```csharp
    void Foo(ref int x) { x = 10; }   // must be initialized before passingvoid Bar(out int x) { x = 10; }   // need not be initialized before, must be assigned inside
    ```
    
- **abstract vs interface (say this fast):** abstract class = partial implementation + state + single inheritance; interface = pure contract + multiple implementation.
- **Value vs reference type, one-liner:** value type copies data, reference type copies the pointer/reference to same object.

---

Good luck for tomorrow. Sabse zyada asked : **value vs reference types**, **virtual/override/sealed**, **abstract vs interface**, **boxing/unboxing**, **properties**, **exception handling**, and a basic **LINQ** one-liner. In agar 6 topics ko confidently bol pao, 80% interview cover ho jaega.



---



## String vs StringBuilder -
string is immutable ( a new string is created with any change )
StringBuilder can append without creating new string thus saving cost

| **Feature**           | **String**                                                   | **StringBuilder**                                                     |
| --------------------- | ------------------------------------------------------------ | --------------------------------------------------------------------- |
| **Mutability**        | **Immutable** (cannot be modified after creation).           | **Mutable** (can be modified in place).                               |
| **Memory Allocation** | Creates a **new memory instance** every time it is modified. | Modifies the **same memory instance** without allocating new objects. |
| **Performance**       | Faster/lighter for fixed or single values.                   | Faster/efficient when performing frequent string modifications.       |

```csharp
string str1 = "Interview";
str1 = str1 + " Happy"; // Creates a new string instance in memory
Console.WriteLine(str1); // Output: Interview Happy



using System.Text;

StringBuilder str2 = new StringBuilder();
str2.Append("Interview");
str2.Append(" Happy"); // Modifies the existing instance in memory

Console.WriteLine(str2.ToString()); // Output: Interview Happy
```


---


## exception handling

```csharp
1. we can have only try with finally to close connection
2. we can have multiple catch blocks --- but only 1 will be executed
3. Throw ex will change stack trace whereas Throw preserves it whole.
   
   try
{
    // Your code here
}
catch (Exception ex)
{
    // 'ex' contains all error data
    Console.WriteLine($"Error: {ex.Message}");
}

```