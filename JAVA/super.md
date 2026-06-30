super is a ref variable, referencing parent object.

uses ->
### 1. access parent's instance variable
### 2. access parent's instance method
### 3. access parent's constructor -
	{ super() }
#### Constructor chaining -
- JVM auto inserts super() { only default parent constructor } at the very beginning of child constructor.
- **IMP -** if the parent does not have a default constructor, code will throw error.
- So, in that case, an explicit super(arg1, arg2) should be called.

----






### In mmy -

classes str :   animal -> dog -> puppy

now if we do, Puppy p = new Puppy();
#### Toh fir `super()` call kyun ho raha hai?

Aapka `Puppy` ka ek single object apne andar teen 'sections' ya 'layers' lekar baithta hai:

```
[---------------- Heap Memory Block ----------------]
|                                                   |
|  1. Animal Layer (e.g., String name, int age)     |  <-- Parent state
|  2. Dog Layer    (e.g., String breed)             |  <-- Intermediate state
|  3. Puppy Layer  (e.g., int monthsOld)            |  <-- Child state
|                                                   |
[------------------ Single Puppy Object ------------]
```

- **Note -** Memory (Heap) mein sirf aur sirf EK hi object banta hai—Puppy ka
- **Space Kitni Legi?** Yeh single object utni space lega jitni `Animal` + `Dog` + `Puppy` ke saare variables ko milakar chahiye. Space teen guna (3x) nahi hoti, bas saare fields ka total hoti hai.
----








in java, we can only access parent via super
and can't access any grandparent
### ❌ The Error: Why `super.super` doesn't work

In Java, **`super.super` is illegal syntax.** The compiler will throw errors like `expected` or `not a statement` because Java strictly prohibits a grandchild class from directly skipping its immediate parent to access the grandparent class's variables or methods.

#### The Concept: Why did Java designers block this?

Java strictly enforces **Encapsulation** and **Method Overriding**. If `Dog` overrode a behavior or variable of `Animal`, it did so for a reason (e.g., to specialize it). If Java allowed `Puppy` to bypass `Dog` and call `Animal` directly via `super.super`, it would break the contract of inheritance. The parent class (`Dog`) loses control over what its child (`Puppy`) can see and modify.