
JavaScript classes are syntactical sugar over the existing prototype-based inheritance. While they look like classes from Java or C++, they behave differently under the hood.

### 1. The Prototype Foundation

- A class is essentially a function. When you define `class User {}`, you are creating a constructor function.
- Methods defined inside the class block are attached to `User.prototype`, not the instance itself.
  {`to save memory`}

### 2. Core Mechanics

- **Constructor:** The initialization engine. It runs automatically when you call `new`.
- **Instance Methods:** Defined directly in the class body. Shared via the prototype chain to save memory.
- **Static Methods/Fields:** Defined with the `static` keyword. They belong to the class constructor itself, not instances (e.g., `User.compare(a, b)`).
- **Private Members:** Prefixing a field or method with `#` (e.g., `#password`) makes it inaccessible outside the class scope. This is enforced at the language level, unlike the `_` convention.


- no let or const is used as the js engine knows the variable belongs to class

```js
class BankAccount {
  // Private field
  #balance = 0;

  constructor(owner) {
    this.owner = owner;
  }

  deposit(amount) {
    if (amount > 0) {
      this.#balance += amount;
      this.#log(`Deposited: ${amount}`);
    }
  }

  // Private method
  #log(message) {
    console.log(`[Transaction Log]: ${message}`);
  }

  get balance() {
    return `Your balance is $${this.#balance}`;
  }
}

const account = new BankAccount("Alice");
account.deposit(100);

console.log(account.balance); // "Your balance is $100"

// These will throw SyntaxErrors or return undefined:
// console.log(account.#balance); 
// account.#log("Hacked!");
```







### 3. Inheritance & `super`

Using `extends` establishes a prototype link between the child and parent.

- `super()` must be called in the child constructor before accessing `this`. It calls the parent’s constructor.
- `super.method()` allows you to call methods from the parent class within the child.

### 4. Getters and Setters

Use `get` and `set` to intercept property access. This allows you to execute logic (like validation) while treating the property as a simple variable.

```js
class Thermostat {
  constructor(celsius) {
    // Internal private storage
    this.#celsius = celsius;
  }
  
  #celsius;

  // Getter: Read-only access to Fahrenheit
  // Computed on the fly
  get fahrenheit() {
    return (this.#celsius * 9) / 5 + 32;
  }

  // Setter: Logic and Validation
  set fahrenheit(value) {
    if (value < -459.67) {
      console.error("Temperature below absolute zero!");
      return;
    }
    this.#celsius = ((value - 32) * 5) / 9;
  }

  get celsius() {
    return this.#celsius;
  }
}

const oven = new Thermostat(20);

// Use like a property, not a function (no parentheses)
console.log(oven.fahrenheit); // 68

oven.fahrenheit = 400; // Calls the setter
console.log(oven.celsius);    // 204.44...
```