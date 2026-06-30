In JavaScript, **`this` is not a regular variable**; it is ==a special keyword that dynamically points to an object depending on how a function is called==. Its value is determined at runtime based on the execution context.

### How `this` Acts in Different Contexts

The value of `this` changes depending on the execution context:

- **Inside an Object Method**: Points to the object that owns the method.
- **Inside a Regular Function**: Points to the global object (`window` in browsers).
- **Inside Strict Mode (`"use strict";`)**: Evaluates to `undefined` inside regular functions.
- **Inside Arrow Functions**: Does not have its own `this` context. It inherits it from the surrounding code.
- **Inside an Event Listener**: Points directly to the HTML element that received the event.

---

### Manual Overrides

Developers can manually assign the reference of `this` using three explicit methods:

- **`call()`**: Invokes a function immediately, passing the `this` context as the first argument.
- **`apply()`**: Works like `call()`, but accepts extra arguments as an array.
- **`bind()`**: Returns a completely new function permanently bound to the chosen object.