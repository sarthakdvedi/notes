2 kahani h -> constructor ki,   and    object ki

#### Papa -
**Function() -** constructor ka papa,  { every object uses a constructor   -->  at top papa hi milega}
**Object -** Prototypal inheritance ka papa, { inheritance k top p }


- prototype -> is the actual data (object having methods and values)
- `__proto__` -> is the link
- Like:  `child.__proto__ === papa.prototype`

### My understanding -
1. har type ka obj ek constructor fn se banta h
2. each constructor fn have it's `prototype` toolbox property with it
   { `of the same type of what it creates ---> like Function ka prototype bhi ek function h,   and Array ka prototype bhi ek array hi hoga }.
3. each type of object in js have `__proto__` field.
4. whenever, the constructor fn creates anything, it simply attaches that `prototype` toolbox to the `__proto__` field of it's creation.


#### IMP POINTS -
- The Prototype Chain --> `.prototype` toolbox **copy nahi hota**, sirf **link** hota hai.
- Searching logic --> pehle apne obj m dhundo, nahi mila to `__proto__` ke raaste `Array.prototype` m jao
  {`Isse memory bachti hai`}

---














### .prototype v/s .__ proto __
The `prototype` property is an **object** toolkit that is shared by all instances created by a constructor function.

Think of it like this:

- **The Function (`Object`)**: The machine that builds new objects.
- **The `prototype` (`Object.prototype`)**: The shared toolbox that the machine attaches to every object it builds.

When you create a new object using `{}`, JavaScript doesn't copy all methods (like `toString`) into that new object. Instead, it gives the new object a hidden link (the "prototype chain") to `Object.prototype`.

Only **functions** have a `prototype` property because only functions can act as constructors (builders) for new objects.

---





Almost every object has a `__proto__` property, but there is one notable exception.
### 1. The Rule

By default, every object created in JavaScript (objects, arrays, functions) has a `__proto__` link that points to the `prototype` of the function that created it.

### 2. The Exception: `null`

The only object that does **not** have a `__proto__` link is `Object.prototype` itself. It is the end of the chain.

#### js

Object.prototype.__proto__; // null

Use code snippets with caution

### 3. Objects with no Prototype

You can manually create an object that has no `__proto__` at all (not even the standard Object methods like `.toString()`) by using `Object.create(null)`:

#### js

const pureObj = Object.create(null);

console.log(pureObj.__proto__); // undefined

  

Use code snippets with caution

**Summary:**

- **Constructor Functions** have a `.prototype` property.
- **Objects** have a `[[Prototype]]` internal link (accessed via `__proto__` or `Object.getPrototypeOf()`).
- **`Object.prototype`** is the only standard object where the link is `null`.

---











### Object types -
### 1. The "Plain" Object (`Object`)

This is the base type. Every other object type below inherits from this.

- **Example**: `const user = { name: "Alice" };`
- **Link**: `user.__proto__ === Object.prototype`

### 2. The "Callable" Object (`Function`)

Functions are objects with the internal capability to be "called" or "executed."

- **Example**: `function add(a, b) { return a + b; }`
- **Link**: `add.__proto__ === Function.prototype`
- **Note**: This is why `Array`, `String`, and `Number` constructors have `__proto__` pointing to `Function.prototype`.

### 3. "Collection" Objects

These are specialized objects built for handling data sets.

- **Arrays**: Specialized for ordered lists. `[1, 2].__proto__ === Array.prototype`.
- **Maps & Sets**: Modern collections for unique values or key-value pairs.
- **Dates & RegEx**: Objects specialized for time and pattern matching.

### 4. "Wrapper" Objects

JavaScript temporarily wraps primitives (strings, numbers, booleans) in these objects so you can call methods on them.

- **String Object**: `new String("hi")`
- **Number Object**: `new Number(42)`
- **Boolean Object**: `new Boolean(true)`

### 5. "Buffer" Objects

Low-level objects used for handling raw binary data.

- **Example**: `ArrayBuffer`, `Uint8Array`.




---



### Bhot jaruri baat -

- **Jis constructor ka jo "kaam" hai, uska toolbox (prototype) bhi waisa hi dikhna chahiye.**
- kyoki Function ek constructor function h and functions are objects in js. so `Function.__proto__` should be equal to `Function.prototype` as Function itself is the constructor function of Function
  { `as we know each constructor fn have it's `prototype` toolbox with it.` }


JavaScript designers decided that the "toolbox" for all functions (`Function.prototype`) should itself be a **function**. That is why when you log `Array.__proto__`, you see `ƒ () { [native code] }`.


---


### Who got prototype property ?

In standard JavaScript, **yes**, only functions (specifically those that can be used as constructors) have a `.prototype` property.

Here is the precise breakdown of who has it and who doesn't:

### 1. Standard Functions (Yes)

Any regular function defined with the `function` keyword has a `.prototype` property by default.

### 2. Built-in Constructors (Yes)

All built-in constructors like `Object`, `Array`, `Function`, `Date`, and `Number` have it. This is where they store the methods that their instances use.

### 3. Arrow Functions (No)

Arrow functions are designed to be lightweight and **cannot** be used as constructors. Therefore, they do not have a `.prototype` property.

### 4. Objects/Instances (No)

Objects created by constructors (like `const obj = {}` or `const arr = []`) do **not** have a `.prototype` property. They only have the hidden `[[Prototype]]` link (accessed via `__proto__`).

### 5. Classes (Yes)

Classes in ES6 are technically "sugar" over constructor functions, so they also have a `.prototype` property.

---
