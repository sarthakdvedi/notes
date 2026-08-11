

baat ye hai -

jiska object bana hai ( container bhaad m gaya )
-----> uska hi method run hona chahiye

par

compiler dumb h --
so -> jiska bhi pointer ( container ) bana hota hai
compiler uspe bind kar deta hai

telling compiler --
to hum virtual keyword use karte h
- jab bhi compiler virtual dekhta h, to vo dumbly early bind nahi karta
- and runtime pe jo main object bana hota hai ( ignoring the container object ), uska (Correct) wala method hi run karta h



---


# trick -

## w/o virtual -
jo left m h, dumbly uska call

## w virtual -
jo right p real object h, uska call intelligently (ignoring dumb early binding)



```cpp
// upcasting
parent *p = new child();

// downcasting
child *ptr = new parent(); // error dega

parent *p1 = new parent();
child *p2 = (child*)p1; // typecast kar lia -- ab nahi dega error
```



---


## what happens if `virtual` is used -

### simple bhasha m (100% accurate) -
1. if any virtual function h class m to Vtable create hoga --- usme bhi, if virtual method overrided h to overrided wale ko hi point karega
2. y Vtable static hota h or only class k lie hota h
3. ab whenever an object is created, during constructor, vptr is initialised in the object created that points to it's own class's Vtable.
4. y vptr se hi pata chalta hai, ki which function to exe at runtime.






bird (parent) ---> sparrow (child)

- At compile time, the compiler generates **one static Virtual Table (vtable)** for every class that contains at least one `virtual` function.
- These vtables exist in the static data segment of your compiled binary before the program even runs.

### 1. How the Compiler Builds (child)`Sparrow`'s Vtable at Compile Time

When the compiler parses the code for `class Sparrow : public Bird`, it performs a systematic copy-and-override process for `Sparrow`'s vtable:

1. **Inherit the Base Layout:** The compiler looks at the base class `Bird`'s vtable layout:
2. **Check for Overrides:** The compiler scans the definition of `Sparrow` to see if it overrides any of these virtual functions.
3. `Sparrow` implements `void fly() override`.
4. Therefore, at **compile time**, the compiler overwrites Slot 1 in`Sparrow`'s vtable layout with the function pointer pointing to `Sparrow::fly()`.

### 2. Where is `vptr` stored?

It is stored **inside the memory layout of the created object itself**.

- When you instantiate an object of a class that has virtual functions (e.g., `Bird *b = new Sparrow();`), the compiler silently inserts a hidden member variable—the `vptr`—at the very beginning of that object's memory allocation.
    
- Because `vptr` is stored inside the object, **it increases the `sizeof` the object** by the size of a pointer

### 3. When is `vptr` created and initialized?

- **Allocation (Created):** The memory space for `vptr` is allocated **at runtime when the object itself is created** in memory (either on the stack or dynamically on the heap via `new`).
    
- **Initialization:** The `vptr` is set to point to the correct static VTable **during the object's constructor execution**.

---

